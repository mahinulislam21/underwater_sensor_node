php code for website database:


<?php

include ('db_config.php');

$db_select = "SELECT * FROM led WHERE id = 1";

$result = $db->query($db_select);

$row = $result->fetch_assoc();

$LED = $row['status'];

echo $LED;

if (isset($_POST['btn_led_01'])){

    echo '<meta http-equiv="refresh" content="0" />';



	if ($LED=='ON'){

		$db_insert = "UPDATE led SET status='OFF' WHERE id=1";

		if (mysqli_query($db,$db_insert)){

			$add_record = "Add New Record";

		}

		else{

			echo "Error :" .$db_insert."<br>".mysqli_connect_error($db);

		}

	}else{

		$db_insert = "UPDATE led SET status='ON' WHERE id=1";

		if (mysqli_query($db,$db_insert)){

			$add_record = "Add New Record";

		}

		else{

			echo "Error :" .$db_insert."<br>".mysqli_connect_error($db);

		}

	}

}



?>

<html>

<style>

*{

	padding: 0;

	margin: 0;

	font-family: "Times New Roman", Times, serif;

}

#wrapper{

	margin-top: 50px;

	padding: 0;

}

#container{

	margin: auto;

	background: #00b0f2;

	width: 650px;
    
    border: 2px black;
    
    border-radius: 25px;
    
	height: 620px;

	box-shadow: 1px 1px 5px 0px #000;

}

#mid-menu{

	margin: auto;

	width: 350px;

	height: auto;

}

#mid-menu input{

	float: left;

	width: 100%;

	height: 50px;

	margin-top: 10px;

	padding-left: 10px;

	font-size: 18px;
	
	

}

#logo-menu{

	width: 100%;

	height:200px;

}

#btn-login{

	margin: auto;

	width: 350px;

	height: 50px;

	float: left;


}

#btn-led {

	margin: auto;

	width: 100%;

	height: 50px;



}

#btn-led button{

	font-size: 18px;

	width: 100%;

	height: 100%;
	
	border: 2px black;
    
    border-radius: 25px;

}

</style>

<body style = "background: Black ">

	<div id="wrapper">

	<div id="container">

	<div id="mid-menu">

						<div id="logo-menu"></div>

							<form method="post" action="db.php">

								<div id="btn-login"><div id="btn-led"><button type="submit" name="btn_led_01"><?php echo $LED;?></button>

								</div>

							</div>

							</form>

						</div>

				</div>

	</div>

</body>

</html>


<?php

define('DBHOST', 'localhost');

define('DBUSER', 'id12904920_nahin');

define('DBPASS', '12345');

define('DBNAME', 'id12904920_underwater_iot');

$db = mysqli_connect(DBHOST,DBUSER,DBPASS,DBNAME);

if (!$db){

	die("Connection Failed: ". mysqli_connect_error());

} ?>



<?php  
      //export.php  
 if(isset($_POST["export"]))  
 {  
      $connect = mysqli_connect("localhost", "id12904920_nahin", "12345", "id12904920_underwater_iot");  
      header('Content-Type: text/csv; charset=utf-8');  
      header('Content-Disposition: attachment; filename=data.csv');  
      $output = fopen("php://output", "w");  
      fputcsv($output, array('id', 'sensor', 'location', 'value1', 'value2', 'value3' , 'reading_time'));  
      $query = "SELECT * from SensorData ORDER BY id DESC";  
      $result = mysqli_query($connect, $query);  
      while($row = mysqli_fetch_assoc($result))  
      {  
           fputcsv($output, $row);  
      }  
      fclose($output);  
 }  
 ?>  


<html>
    <head>
        <title>Under-Water Monitoring System</title>
        <style>
            li {
                width : 60%;
                padding-top :5%;
                padding-bottom :5%;
                background-color:DeepSkyBlue;
                margin-top :5%;
                margin-bottom : 5%;
                font-size:30px;
                list-style : none;
                border: 2px DeepSkyBlue;
                border-radius: 25px;
                }
            h1{
              color:DeepSkyBlue;
              text-decoration:underline;
              
            }
            a{
             text-decoration:none;
             color :Black;
            }
            ul{
               margin-top :5%;
               margin-bottom : 5%;
               margin-left:30%;
               margin-right:10%;
            }
        </style>
    </head>
    <body style = "background-color:Black ; text-align:center">
        <h1>Under-Water Monitoring System</h1>
        <ul>
            <li><a href = "https://hexagonal-millimete.000webhostapp.com/show.php">Complete Table</a></li>
            <li><a href = "https://hexagonal-millimete.000webhostapp.com/Plot.php">Chart</a></li>
            <li><a href = "https://hexagonal-millimete.000webhostapp.com/db.php">Control Panel</a></li>
        </ul>
    </body>
</html>




<?php
$connection=mysqli_connect("localhost","id12904920_nahin","12345","id12904920_underwater_iot"); //servername,username,password,database_name
if($_SERVER['REQUEST_METHOD'] === 'POST'){
	$username=$_POST['username'];
	$password=$_POST['password'];
	$sql="SELECT password FROM admin WHERE username='$username'"; 
	$result=mysqli_query($connection,$sql);
	$pass=mysqli_fetch_array($result,MYSQLI_NUM);
	if($password===$pass[0]){
	    header('Location:Home.php');
	    
	}
	else {
	    echo "<script type='text/javascript'>alert('Incorrect Password,Try again');</script>";
	}
}

?>
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="icon" href="icon.png">
  <title>LOG IN</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.6.3/css/all.css" integrity="sha384-UHRtZLI+pbxtHCWp1t77Bi1L4ZtiqrqD80Kn4Z8NTSRyMA2Fd33n5dQ8lWUE00s/" crossorigin="anonymous">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
	<style type="text/css">
		td,th{
			text-align:center;
		}
		img[src="https://cdn.000webhost.com/000webhost/logo/footer-powered-by-000webhost-white2.png"]{
		    display:none;
		    
		}
		body{
			background-image: url('a.jpg');
			background-size: cover;
			background-attachment: fixed;
			background-repeat: no-repeat;
			color:white;
			/*background-size: 100% 100%;*/
		}
		#all{
			/*background-color:blue;*/
			position: absolute;
			transform: translate(-50%,-50%);
			text-align:center;
			top: 46%;
			left: 50%;
			width: 60%;
			height: 400px;
			color: white;
		}
		input{
			border-radius: 6px;
			background-color: white;
			width: 50%;
			height: 40px;
		}
		label{
			font-weight: bold;
			font-size: 15px;
		}
	</style>
</head>
<body>
	<div class="container" id="all">
		<br>
		<br>
		<br>
		<br>
		<h1>WELCOME BACK,Admin</h1>
		<form method="POST" action="index.php" autocomplete="off">
			<label>USERNAME</label><br>
			<input type="text" name="username" required><br><br>
			<label>PASSWORD</label><br>
			<input type="password" name="password" required><br><br>
			<input type="submit" name="submit" style="width: 10%;">
		</form>
	</div>
</body>


<?php

$servername = "localhost";

// REPLACE with your Database name
$dbname = "id12904920_underwater_iot";
// REPLACE with Database user
$username = "id12904920_nahin";
// REPLACE with Database user password
$password = "12345";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 

$sql = "SELECT id, value1, value2, value3, reading_time FROM SensorData order by reading_time desc limit 40";

$result = $conn->query($sql);

while ($data = $result->fetch_assoc()){
    $sensor_data[] = $data;
}

$readings_time = array_column($sensor_data, 'reading_time');

// ******* Uncomment to convert readings time array to your timezone ********
/*$i = 0;
foreach ($readings_time as $reading){
    // Uncomment to set timezone to - 1 hour (you can change 1 to any number)
    $readings_time[$i] = date("Y-m-d H:i:s", strtotime("$reading - 1 hours"));
    // Uncomment to set timezone to + 4 hours (you can change 4 to any number)
    //$readings_time[$i] = date("Y-m-d H:i:s", strtotime("$reading + 4 hours"));
    $i += 1;
}*/

$value1 = json_encode(array_reverse(array_column($sensor_data, 'value1')), JSON_NUMERIC_CHECK);
$value2 = json_encode(array_reverse(array_column($sensor_data, 'value2')), JSON_NUMERIC_CHECK);
$value3 = json_encode(array_reverse(array_column($sensor_data, 'value3')), JSON_NUMERIC_CHECK);
$reading_time = json_encode(array_reverse($readings_time), JSON_NUMERIC_CHECK);

/*echo $value1;
echo $value2;
echo $value3;
echo $reading_time;*/

$result->free();
$conn->close();
?>

<!DOCTYPE html>
<html>
<meta name="viewport" content="width=device-width, initial-scale=1">
  <script src="https://code.highcharts.com/highcharts.js"></script>
  <style>
    body  {
        min-width: 310px;
    	max-width: 1280px;
    	height: 500px;
        margin: 0 auto;
    }
    h2 {
      font-family: Arial;
      font-size: 2.5rem;
      text-align: center;
    }
  </style>
  <body style = "background-color : Black">
    <h2 style = "color : DeepSkyBlue">Water Monitor</h2>
    <div id="chart-pH" class="container"></div>
    <div id="chart-temperature" class="container"></div>
    <div id="chart-proximity" class="container"></div>
<script>

var value1 = <?php echo $value1; ?>;
var value2 = <?php echo $value2; ?>;
var value3 = <?php echo $value3; ?>;
var reading_time = <?php echo $reading_time; ?>;

var chartT = new Highcharts.Chart({
  chart:{ renderTo : 'chart-pH' },
  title: { text: 'Water pH' },
  series: [{
    showInLegend: false,
    data: value1
  }],
  plotOptions: {
    line: { animation: false,
      dataLabels: { enabled: true }
    },
    series: { color: '#059e8a' }
  },
  xAxis: { 
    type: 'datetime',
    categories: reading_time
  },
  yAxis: {
    title: { text: 'pH' }
  },
  credits: { enabled: false }
});

var chartH = new Highcharts.Chart({
  chart:{ renderTo:'chart-temperature' },
  title: { text: 'Water Temperature' },
  series: [{
    showInLegend: false,
    data: value2
  }],
  plotOptions: {
    line: { animation: false,
      dataLabels: { enabled: true }
    }
  },
  xAxis: {
    type: 'datetime',
    //dateTimeLabelFormats: { second: '%H:%M:%S' },
    categories: reading_time
  },
  yAxis: {
    title: { text: 'Temperature(C)' }
  },
  credits: { enabled: false }
});


var chartP = new Highcharts.Chart({
  chart:{ renderTo:'chart-proximity' },
  title: { text: 'Proximity' },
  series: [{
    showInLegend: false,
    data: value3
  }],
  plotOptions: {
    line: { animation: false,
      dataLabels: { enabled: true }
    },
    series: { color: '#18009c' }
  },
  xAxis: {
    type: 'datetime',
    categories: reading_time
  },
  yAxis: {
    title: { text: 'Proximity' }
  },
  credits: { enabled: false }
});

</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<title>Data Table</title>
<style>
table, th, td {
  border: 4px solid black;
  background-color : DeepSkyBlue;
  font-size : 20px
}
h1{
    text-decoration:underline;
    color : DeepSkyBlue;
}
</style>
</head>
<body style = "background-color : Black ; text-align: center">
<?php

$servername = "localhost";

// REPLACE with your Database name
$dbname = "id12904920_underwater_iot";
// REPLACE with Database user
$username = "id12904920_nahin";
// REPLACE with Database user password
$password = "12345";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 

$sql = "SELECT id, sensor, location, value1, value2, value3, reading_time FROM SensorData ORDER BY id DESC";
echo '<h1>Data Status</h1>';

echo '<br />  
            <form method="post" action="export.php" align="center">  
            <input type="submit" name="export" value="CSV Export" class="btn btn-success" />  
            </form>  
            <br />  
      <table cellspacing="5" cellpadding="10" style="margin:0 0 0 0 ; width:100%"">
      <tr style="background-color:teal"> 
        <td>ID</td> 
        <td>Sensor</td> 
        <td>Location</td> 
        <td>Value 1</td> 
        <td>Value 2</td>
        <td>Value 3</td> 
        <td>Timestamp</td> 
      </tr>';
 
if ($result = $conn->query($sql)) {
    while ($row = $result->fetch_assoc()) {
        $row_id = $row["id"];
        $row_sensor = $row["sensor"];
        $row_location = $row["location"];
        $row_value1 = $row["value1"];
        $row_value2 = $row["value2"]; 
        $row_value3 = $row["value3"]; 
        $row_reading_time = $row["reading_time"];
        // Uncomment to set timezone to - 1 hour (you can change 1 to any number)
        //$row_reading_time = date("Y-m-d H:i:s", strtotime("$row_reading_time - 1 hours"));
      
        // Uncomment to set timezone to + 4 hours (you can change 4 to any number)
        //$row_reading_time = date("Y-m-d H:i:s", strtotime("$row_reading_time + 4 hours"));
      
        echo '<tr> 
                <td>' . $row_id . '</td> 
                <td>' . $row_sensor . '</td> 
                <td>' . $row_location . '</td> 
                <td>' . $row_value1 . '</td> 
                <td>' . $row_value2 . '</td>
                <td>' . $row_value3 . '</td> 
                <td>' . $row_reading_time . '</td> 
              </tr>';
    }
    $result->free(); 
}

$conn->close();
?> 
</table>
</body>
</html>



<?php

header("Access-Control-Allow-Origin: *");

header("Content-Type: application/json; charset=UTF-8");







//Creating Array for JSON response

$response = array();



$servername = "localhost";

$username = "id12904920_nahin";

$password = "12345";

$dbname = "id12904920_underwater_iot";



// Create connection

$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection

if ($conn->connect_error) {

    die("Connection failed: " . $conn->connect_error);

}







 // Fire SQL query to get all data from led

 if (isset($_GET["id"])) {

     $id = $_GET['id'];



      // Fire SQL query to get weather data by id

     $result = $conn->query("SELECT * FROM led WHERE id = '$id'");



 	//If returned result is not empty

     if (!empty($result)) {



         // Check for succesfull execution of query and no results found

         if (mysqli_num_rows($result) > 0) {



 			// Storing the returned array in response

             $result = mysqli_fetch_array($result);



 			// temperoary user array

             $led = array();

             $led["id"] = $result["id"];

             $led["status"] = $result["status"];





             // Show JSON response

             echo json_encode($led);

         } else {

             // If no data is found

             $response["success"] = 0;

             $response["message"] = "No data on led found";



             // Show JSON response

             echo json_encode($response);

         }

     } else {

         // If no data is found

         $response["success"] = 0;

         $response["message"] = "No data on led found";



         // Show JSON response

         echo json_encode($response);

     }

 } else {

     // If required parameter is missing

     $response["success"] = 0;

     $response["message"] = "Parameter(s) are missing. Please check the request";



     // echoing JSON response

     echo json_encode($response);

 }

 ?>


<?php

$servername = "localhost";

// REPLACE with your Database name
$dbname = "id12904920_underwater_iot";
// REPLACE with Database user
$username = "id12904920_nahin";
// REPLACE with Database user password
$password = "12345";

// Keep this API Key value to be compatible with the ESP32 code provided in the project page. 
// If you change this value, the ESP32 sketch needs to match
$api_key_value = "1234";

$api_key= $sensor = $location = $value1 = $value2 = $value3 = "";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $api_key = test_input($_POST["api_key"]);
    if($api_key == $api_key_value) {
        $sensor = test_input($_POST["sensor"]);
        $location = test_input($_POST["location"]);
        $value1 = test_input($_POST["value1"]);
        $value2 = test_input($_POST["value2"]);
        $value3 = test_input($_POST["value3"]);
        
        // Create connection
        $conn = new mysqli($servername, $username, $password, $dbname);
        // Check connection
        if ($conn->connect_error) {
            die("Connection failed: " . $conn->connect_error);
        } 
        
        $sql = "INSERT INTO SensorData (sensor, location, value1, value2, value3)
        VALUES ('" . $sensor . "', '" . $location . "', '" . $value1 . "', '" . $value2 . "', '" . $value3 . "')";
        
        if ($conn->query($sql) === TRUE) {
            echo "New record created successfully";
        } 
        else {
            echo "Error: " . $sql . "<br>" . $conn->error;
        }
    
        $conn->close();
    }
    else {
        echo "Wrong API Key provided.";
    }

}
else {
    echo "No data posted with HTTP POST.";
}

function test_input($data) {
    $data = trim($data);
    $data = stripslashes($data);
    $data = htmlspecialchars($data);
    return $data;
}



code description:

This website is developed using php and sql programing language.  Here we can see to enter in the website username and password is needed which makes the website more secure. First page of the website leads to the file management and control option of the node.
The link of the website is- http://hexagonal-millimete.000webhostapp.com
Username: nahin
Password: 01753525338
After giving the proper username and password admin can reach to the second page of the site which gives three more options. As we can see in Fig 3.7 the options are- complete table, chart and control panel
This option helps to see the excel sheet of all the sensor reading with real-time processing. There is an option in the page (CSV export) to download the table as a excel sheet in electronics devices for further analysis. We can see the real-time pH, temperature, location and proximity from the table of the website.This option helps to see the graphical representation of all the sensor reading. There is an option on the graph to click to see the real-time value of the sensor reading in the page. There are three graphical representation of sensors reading on the website. All the pH, temperature and PIR sensor reading of the table are shown in a graphical form in this section.This option of the website is introduced to control the UWSN when it is localized underwater. The sensor node is placed under water surface for a long time to monetize aquatic environment. During this period of time if we displace the node from its location for manual controlling it will start giving dubious results. So, it is essential to introduce a wireless controlling option to the node. Control panel option of the website comes forward on this problem. A dynamic power management approach was also introduced to run the device on minimum power. 



code output: code output is shown in picture 1,2,3,4,5,6,7



