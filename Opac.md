# 4.4: Creating a Bare Bones OPAC

This was an interesting assignment. Forgive me that I didn't follow the directions entirely.

I wanted to experiment a bit with creating a RESTful endpoint to access the data.

Stack:
  - MySQL Database as data layer
  - PHP as middleware
  - Javascript to query and manage data
  - Html as presentation layer

Basically, the Html form is manaaged by opac.js. Search data is added via Html, processed by JS to create a json response (a promise) to the Php (which, of course, 
queries the database and then returns an array of arrays... but in this case usually just a single array.

### JS
```
$widget_info_data = get_json_response(info_http).then((data) => {

            var n = data.length;                            
            var result_text = "";
            var results_div = document.getElementById("results");

            if (n > 0) {
        
                for (const x of data) {
                    console.log(x);
                    result_text += x['id'];
                    result_text += x['author'];
                    result_text += x['title'];
                    result_text += x['publisher']
                    result_text += x['copyright'];

                }

                results_div.innerHTML = result_text;        



            } else {

                // show_hide_widget_page_elements('none');
                display_error_info({type:'info', msg:'No results were returned for that query'});

            }
        });
```

### Php

```
 $conn = get_db_conn();
    mysqli_select_db($conn, DB_DATABASE) or die("Could not open database");
    $query1 = "select * from books where title like '%$search_value%'";
    $result1 = mysqli_query($conn, $query1);

    $bookArray = array();

    if (mysqli_num_rows($result1)  == 0) {

        $query2 = "select * from books where author like '%$search_value%'";
        $result2 = mysqli_query($conn, $query2);
        
        if (mysqli_num_rows($result2)  > 0) {
            while($row = $result2->fetch_assoc()) {
                $bookArray[] = $row;
            }   
        } else {
            $bookArray.array_push("id:none");
        }     
    } else {

        while($row = $result1->fetch_assoc()) {
                $bookArray[] = $row;
        }
    };

    header('Content-type: application/json');
    echo json_encode( $bookArray);
```
