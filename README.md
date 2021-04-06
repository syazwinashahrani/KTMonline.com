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


<body>
			
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



</body>

use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

include 'PHPMailer/src/Exception.php';
include 'PHPMailer/src/PHPMailer.php';
include 'PHPMailer/src/SMTP.php';

$mail = new PHPMailer(true);try {//Server settings
$mail->isSMTP();
$mail->Host       = 'smtp.gmail.com';
$mail->SMTPAuth = true;
$mail->Username   = 'syztripinmy@gmail.com' ;
$mail->Password   = 'tripinmy2021' ;
$mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
$mail->Port       = 587;

$mail->setFrom('syazwinashahrani@gmail.com');// send to one recepient only, name is optional 2nd argument
$mail->addAddress($email);
$mail->isHTML(true);
$mail->Subject = 'KTM SDN BHD' ;
$mail->Body    = "<p>Hi Mr/Mrs $f_name $l_name,</p>
<p>You have successfully purchase KTM ticket from <b>$routes[$origin]</b> to <b>$routes[$destination]</b></p>
<p>For more information, please contact management directly.</p>
<br>
<h4>TICKET - ITINERY</h4>

<table border='1'>
<tr>
<th>From</th>
<th>To</th>
<th>Category</th>
</tr>
<tr>
<td>$routes[$origin]</td>
<td>$routes[$destination]</td>
<td>$category</td>
</tr>
</table>

<br>
<h4>Passenger details</h4>
<table>
<tr>
<td>Name</td>
<td>:</td>
<td>$f_name $l_name</td>
</tr>
<tr>
<td>IC Number</td>
<td>:</td>
<td>$icnum</td>
</tr>
<tr>
<td>Email</td>
<td>:</td>
<td>$email</td>
</tr>
</table>

<p> Thank You for using KTM.com! </P>" ;
$mail->send();

echo "<p>Message has been sent to $email.</p>";
}
catch (Exception $e)
{
echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}	
?>
