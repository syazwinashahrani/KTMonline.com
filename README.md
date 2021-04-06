# KTMonline.com
KTM system is a website that provide a user to purchase train ticket online

<?php
session_start();
if(isset($_SESSION['name'])){}
	else{
		header("location:login1.php");
		
	}
$tbl_name="users"; // Table name
$name=$_SESSION['name'];

require('firstimport.php');

mysqli_select_db($conn,"$db_name") or die("cannot select db");

$result=mysqli_query($conn,"SELECT * FROM $tbl_name WHERE f_name='$name'");
$row=mysqli_fetch_array($result);


?>

<!DOCTYPE html>
<html>
<head>
	<title> Profile </title>
	<link rel="shortcut icon" href="images/favicon.png"></link>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="">
    <meta name="author" content="">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Open+Sans:300,300i,400,600">
 <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.6/css/all.css">
	<link href="//netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="stylesheet">
	<link href="css/bootstrap.min.css" rel="stylesheet">
	</link>
	<link href="css/Default.css" rel="stylesheet">
	</link>
	<script type="text/javascript" src="js/jquery.js"></script>
	<script>
		$(document).ready(function()
		{
			//alert($(window).width());
			var x=(($(window).width())-1024)/2;
			//alert(x);
			$('.wrap').css("left",x+"px");
		});

	</script>
	<script type="text/javascript" src="js/bootstrap.min.js"></script>
	<script type="text/javascript" src="js/bootstrap.js"></script>
	<script type="text/javascript" src="js/man.js"></script>
	
</head>

<body>
	
	<div class="wrap">
		<!-- Header -->
		<div class="header">
			<div style="float:left;width:150px;">
				<img src="images/trainn.png"/>
			</div>		
			<div>
			<div style="float:right; font-size:20px;margin-top:20px;">
			<?php
			 if(isset($_SESSION['name']))
			 {
			 echo "Welcome,".$_SESSION['name']."&nbsp;&nbsp;&nbsp;<a href=\"logout.php\" class=\"btn btn-info\">Logout</a>";
			 }
			 else
			 {
				$_SESSION['error']=15;
				//echo "fgfggy".$_SESSION['error'];
				header("location:login1.php");
			 } 
			 ?>
			</div>
			<div id="heading">
				<a href="index.php">KTM SDN BHD</a>
			</div>
			</div>
		</div>
		<!-- Navigation bar -->
		<div class="navbar navbar-inverse" >
			<div class="navbar-inner">
				<div class="container" >
				<a class="brand" href="index.php" >HOME</a>
				<a class="brand" href="train.php" >FIND ROUTES</a>
				<a class="brand" href="reservation.php">PURCHASE TICKET</a>
				<a class="brand" href="profile.php">PROFILE</a>
				<a class="brand" href="display.php">PURCHASE HISTORY</a>
				</div>
			</div>
		</div>
		
		<div class="span12 well pass1">
			<table style="width:100%;">
			<tr>
				<td><span style="font-weight:bold;font-size:25px;">Profile</span>
				<a id="editp1" style="float:right;margin-right:5%;"class="btn btn-info"> Edit Profile</a></td>
			<tr/>
			
			<tr>
				<td>
					<div class="span8" style="float:left;width:80%;">
					<table class="table">
					<tr><td >First Name : </td> <td style="text-transform:capitalize;"><?php echo $row['f_name']; ?></td></tr>
					<tr><td >Last Name : </td> <td style="text-transform:capitalize;"><?php echo $row['l_name']; ?></td></tr>
					<tr><td>E-Mail : </td> <td><?php echo $row['email'];?></td></tr>
					<tr><td>Dob : </td> <td><?php echo $row['dob']; ?></td></tr>
					<tr><td> Gender :</td> <td><?php echo $row['gender'];?></td></tr>
					<tr><td>Marital Status : </td> <td><?php echo $row['marital']; ?></td></tr>
					<tr><td>Mobile No : </td> <td><?php echo $row['mobile'];?></td></tr>
					<tr><td>Security Question : </td> <td><?php echo $row['ques']; ?></td></tr>
					<tr><td>Answer : </td> <td><?php echo $row['ans']; ?></td></tr>
					<tr><td></td> <td></td></tr>
					</table>
					</div>
				</td>
			</tr>
			
			<tr>
				<td>
				<span style="width:35%;"><a id="cpass">Change Password</a></span>
				<span class="label label-success" id="chang" style="float:right;display:none;">Password Successfully Changed &nbsp;&nbsp;&nbsp;<span>  <!-- display:none; color:#0000ff;-->
				</td>
			</tr>
		</table>
		</div>

		<div class="span12 pass2 " style="display:none;">
		<div class="span4 well">	
		<h2>Change Password</h2>	
		<br/>
		<br/>
				<form action="changepass.php" method="get" onsubmit="return fgth()">
				<label>New Password</label><input id="p1" name ="new1" type="password" class="input-large" onkeyup="return check123()"><span id="ps" ></span></td><br><br>
				<label>Repeat Password</label><input id="p2" name="pass" class="input-large" type="password" onkeyup="checkk()">
				<br /><span id="match" style="color:#ff0000;visibility:hidden;">&nbsp;&nbsp;Password Don't Match</span><br><br> 
				<input id="sub" type="submit" disabled="disabled" class="btn btn-info" value="Change Password">
				</form>
		</div>
		</div>
		
		
		
		<div class="span12 pass3 " style="display:none;">
		<div class="span8 well">
			<table style="width:100%;">
			<tr>
				<td><span style="font-weight:bold;font-size:25px;">Profile</span>

			<tr/>
			
			<tr>
				<td>
					<form action="editprofile.php" method="post" enctype="multipart/form-data">
					<div class="span6" style="float:left;width:80%;">
					<table class="table">
					
					<tr><td >First Name  </td> <td style="text-transform:capitalize; onblur="return name1()"><?php echo $name;?></td></tr>
					<tr><td> Last name </td> <td><input name="ln" type="text" value="<?php echo $row['l_name'];?>"></td></tr>
					<tr><td>E-Mail  </td> <td><input name="mail1" type="mail" value="<?php echo $row['email'];?>"></td></tr>
					<tr><td>Dob  </td> <td><input name="dob1" type="text" value="<?php echo $row['dob'];?>"></td></tr>
					<tr><td>Gender  </td>  <td><input name="gnd1" type="text" value="<?php echo $row['gender'];?>"></td></tr>
					<tr><td>Marital Status </td>  <td><input name="mrt1" type="text" value="<?php echo $row['marital'];?>"></td></tr>
					<tr><td>Mobile No.  </td>  <td><input name="mon1" type="text" value="<?php echo $row['mobile'];?>"></td></tr>
					<tr><td>Security Question  </td>  <td><input name="que1" type="text" value="<?php echo $row['ques'];?>"></td></tr>
					<tr><td>Answer  </td>  <td><input name="ans1" type="text" value="<?php echo $row['ans'];?>"></td></tr>
					<tr><td></td> <td><input type="submit" value="Save Profile" class="btn btn-info"></td></tr>
				
					</table>
					</div>
					</form>
				</td>
			</tr>
			</table>
		</div>
		</div>
	
<footer >
		<div  class="span12 well">
			
			<div style="float:left;margin-left: 50px">
				<p class="text-right text-info"><h5>CONTACT US</h5>
				<p>Legal and Secretarial Services Unit,
				<br>2nd Floor, KTMB Corporate Headquarters,
				<br>Jalan Sultan Hishamuddin,
				<br>50621 Wilayah Persekutuan,
				<br>Kuala Lumpur.</p>
				<p><i class="fas fa-phone"></i> Call Center +603 - 2267 1200</p>
				<p><i class="fas fa-envelope"></i> Email: callcenter@ktmb.com.my</a></p>
			</div>
			
			<div style="float:left;margin-left: 120px">
				<p class="text-right text-info"><h5>QUICK LINK</h5>
				 <a href="http://localhost:84/trains/train.php">Find Route ></a><br><br>
				 <a href="http://localhost:84/trains/reservation.php">Purchase Ticket ></a><br><br>
				 <a href="http://localhost:84/trains/profile.php">Profile ></a><br><br>
				 <a href="http://localhost:84/trains/display.php">Purchase History ></a> 
			</div>
			
			<div style="float:right;margin-right: 50px ">
				<p class="text-right text-info"><h5>FOLLOW US</h5><br>
				<ul>
				<li><a href="http://facebook.com/"><i class="fa fa-facebook"></i></a></li>
				<li><a href="http://linkedin.com/"><i class="fa fa-linkedin"></i></a></li>
				<li><a href="http://twitter.com/"><i class="fa fa-twitter"></i></a></li>
				<li><a href="http://plus.google.com/"><i class="fa fa-google-plus"></i> </a></li>
				</ul>
			</div>

		</div>
		
		<p class="text-center text-info" style="text-align: center">&copy; 2019 Copyright Project Internet Programming.
		<br>Desinged By : Rabiatul, Syazwina, Aliff</p>
</footer>

  
<?php mysqli_close($conn); ?>
 
 
 
 <script type="text/javascript">
$(document).ready(function(){
  $("#cpass").click(function(){
    $(".pass1").fadeOut(1000,"linear",function(){$(".pass2").fadeIn(1000);});
	
  });
});

$(document).ready(function(){
  $("#editp1").click(function(){
    $(".pass1").fadeOut(1000,"linear",function(){$(".pass3").fadeIn(1000);});
	
  });
});

$(document).ready(function(){
  $("#editp2").click(function(){
    $(".pass3").fadeOut(1000,"linear",function(){$(".pass1").fadeIn(1000);});
  });
});


function checkk(){

var p1=document.getElementById("p1").value;
var p2=document.getElementById("p2").value;
//alert(" p1 : "+p1+"  p2 : "+p2);

	if(p1 == p2)
	{document.getElementById("match").style.visibility="hidden";
		document.getElementById("sub").disabled=false;
	}else
	{
		document.getElementById("match").style.visibility="";
		document.getElementById("sub").disabled=true;
	}
}

function check123()
	{
		var c=document.getElementById("p1").value;
		//alert(c.length);
		if(c.length < 8 )
		{
			document.getElementById("ps").innerHTML="<br/><font color=red>password must be atleast 8 - 32 char long</font>";
			return false;
		}
		else
		{
			document.getElementById("ps").innerHTML="";
			return true;
		}
	}
</script>
<?php

if(isset($_SESSION['error']))
{
if($_SESSION['error']==6)
{echo "<script>document.getElementById(\"chang\").style.display=\"\";</script>";
 }
//unset($_SESSION['error']);
}
?>

</body>
  
  
</html>
