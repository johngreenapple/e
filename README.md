<?php
session_start();

require('db.php');
// If form submitted, insert values into the database.
if (isset($_REQUEST['username'])){
        // removes backslashes
	$username = stripslashes($_REQUEST['username']);
        //escapes special characters in a string
	$username = mysqli_real_escape_string($con,$username); 
	$password = stripslashes($_REQUEST['password']);
	$password = mysqli_real_escape_string($con,$password);
        $query = "SELECT * FROM `visitors` WHERE username='$username'
and password='$password'";
	$result = mysqli_query($con,$query) or die(mysqli_error($con));
	$rows = mysqli_num_rows($result);
        if($rows==1){
	    $_SESSION['username'] = $username;
            // Redirect user to index.php
	    header("Location: homepage.php");
	    exit();
         }else{
	echo "<div class='form'>
<h3>Username/password is incorrect.</h3>
<p>Click here to <a href='loginpage.php'>Login</a> </p> </div>";
	}
    }
?>
