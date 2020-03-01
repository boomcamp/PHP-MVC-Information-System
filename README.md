<h1 id="isystem">MVC - Information System </h1>

This is your first MVC activity in which you are going to complete the `missing functionalities` of our `Icontroller.php` and `Imodel.php` below are the important parts that you should aware of in developing a codeigniter applications:


## Routes

It's always necessary to add a readable format in your application's url the basic segments in codeigniter is `hostname/controller/function/parameter1/parameter2`

## Model

Codeigniter models holds data layer and business logic of your application  `isystem/application/Imodel.php`

## Controller

Controller holds all the system process example of that is login/logout process `isystem/application/Icontroller.php`

## Libraries and helpers

Codeigniter supports custom `libraries` and `helpers` it is located under `isytem/application/libraries` and `isytem/application/helpers` and can be loaded inside your controllers `constructor`

Example on how to load helpers

```
public function __construct() 
{
  parent::__construct();
  //Message: Call to undefined function base_url()
  $this->load->helper('url'); 

  //Message: Call to undefined function ouput_to_json()
  $this->load->helper('isystem_helper');
}
```

## Screenshots

Here are the example of forms that you need to complete the functionalities:

Login/Exit System Page:

![login png](screenshots/login.png)

Create Page:

![Create Students](screenshots/create-students.png)

Update Page:

![Update Students](screenshots/update-students.png)

Delete Page:

![Delete Page](screenshots/delete-students.png)


## The views and scripts

Codeiniter support templating and it is located under the `views` folder.

* `/views/includes/header.php - The page header of the system it includes necessary scripts to be used by the system

* `/views/includes/footer.php - Application footer

* `/views/pages/login.php - The login form of the system

* `/views/pages/list.php - Display all students in a table

* `/views/pages/create.php - The create student form

* `/views/pages/update.php - The update student form



# The Initial SetUp

In order to run the application you need to configure the `url segment` and`database connection` accordingly.

1.) Download codeigniter and extract it inside your `/opt/lampp/htdocs` folder then rename it as `isystem`

2.) Update your `isytem/application/config.php` .

<details>
<summary> isytem/application/config.php </summary>

```
$config['index_page'] = '';

$config['base_url'] = 'http://localhost/isystem/';
```

</details>

3.) Add `.htaccess` inside your root directory `isystem/.htaccess` this will remove the `index.php` in the url.

<details>
<summary> isystem/.htaccess </summary>
	
```
RewriteEngine on
RewriteCond $1 !^(index\.php|resources|robots\.txt)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L,QSA]
```

</details>

4.) Create your database `info_db` in your [phpmyadmin](http://localhost/phpmyadmin).

<details>
<summary> info_db </summary>
	
```	
-- phpMyAdmin SQL Dump
-- version 5.0.1
-- https://www.phpmyadmin.net/
--
-- Host: localhost
-- Generation Time: Feb 29, 2020 at 10:12 AM
-- Server version: 10.4.11-MariaDB
-- PHP Version: 7.4.2

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET AUTOCOMMIT = 0;
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `info_db`
--

-- --------------------------------------------------------

--
-- Table structure for table `course`
--

CREATE TABLE `course` (
  `id` int(10) NOT NULL,
  `name` varchar(1000) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `course`
--

INSERT INTO `course` (`id`, `name`) VALUES
(1, 'PHP'),
(2, 'REACT'),
(3, 'PYTHON');

-- --------------------------------------------------------

--
-- Table structure for table `students`
--

CREATE TABLE `students` (
  `id` int(10) NOT NULL,
  `user_id` int(10) NOT NULL,
  `course_id` int(10) NOT NULL,
  `fullname` varchar(1000) NOT NULL,
  `email` varchar(1000) NOT NULL,
  `contact` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `students`
--

INSERT INTO `students` (`id`, `user_id`, `course_id`, `fullname`, `email`, `contact`) VALUES
(1, 1, 2, 'Jino Lacson', 'jino.lacson@boom.camp', '09107375884');

-- --------------------------------------------------------

--
-- Table structure for table `users`
--

CREATE TABLE `users` (
  `id` int(10) NOT NULL,
  `username` varchar(1000) NOT NULL,
  `password` varchar(1000) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `users`
--

INSERT INTO `users` (`id`, `username`, `password`) VALUES
(1, 'jino', '7b5950a50ff66388a63cb14d1cfaeaeb6708230d');

--
-- Indexes for dumped tables
--

--
-- Indexes for table `course`
--
ALTER TABLE `course`
  ADD PRIMARY KEY (`id`);

--
-- Indexes for table `students`
--
ALTER TABLE `students`
  ADD PRIMARY KEY (`id`);

--
-- Indexes for table `users`
--
ALTER TABLE `users`
  ADD PRIMARY KEY (`id`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `course`
--
ALTER TABLE `course`
  MODIFY `id` int(10) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT for table `students`
--
ALTER TABLE `students`
  MODIFY `id` int(10) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT for table `users`
--
ALTER TABLE `users`
  MODIFY `id` int(10) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```

</details>

4.) Configure your database adapter `isytem/application/database.php`.

<details>
<summary> isytem/application/database.php </summary>
	
```
<?php
defined('BASEPATH') OR exit('No direct script access allowed');
$active_group = 'default';
$query_builder = TRUE;

$db['default'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'info_db',
	'dbdriver' => 'mysqli',
	'dbprefix' => '',
	'pconnect' => FALSE,
	'db_debug' => (ENVIRONMENT !== 'production'),
	'cache_on' => FALSE,
	'cachedir' => '',
	'char_set' => 'utf8',
	'dbcollat' => 'utf8_general_ci',
	'swap_pre' => '',
	'encrypt' => FALSE,
	'compress' => FALSE,
	'stricton' => FALSE,
	'failover' => array(),
	'save_queries' => TRUE
);

```
</details>

# The templates

<details>
<summary>  isystem/application/views/includes/header.php </summary>
	
```
<!DOCTYPE html>
<html>
<head>
  <title>Boom Camp - System</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/css/toastr.min.css" />

  <script src="http://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.0.2/js/toastr.min.js"></script>

    <script>

    	  //base url for the script
    	  var url = "<?php echo base_url(); ?>";

    	  /**
    	   * Set delay for redirections
    	   */
    	  function setDelay(loc)
    	  {
    	  	 setTimeout(function(){ 
    	  	 	location.href = loc
    	  	 }, 1000);
    	  }

    	  /**
    	   * A function call that will show "Create Students" form
    	   */
		  function showCreateForm()
		  {
		  	$('#createStudents').modal('show');
		  }

		  /**
    	   * A function call that will show "Update Students" form
    	   */
		  function showEditForm(user_id)
		  {
		  	$('#updateStudents')
		  	.modal('show');
		  	

		  	 $.get(url+"get/"+user_id, function(data, status){
			    $.map(data.msg, function(response) {
				$('#formUpdate select#course_id option[value="'+response.course_id+'"]')
				.attr("selected",true);
		  	
				  $("#formUpdate #user_id").val(response.user_id);
				  $("#formUpdate #username").val(response.username);
				  $("#formUpdate #password").val(response.password);
				  $("#formUpdate #fullname").val(response.fullname);
				  $("#formUpdate #email").val(response.email);
				  $("#formUpdate #contact").val(response.contact);
				});
			 });
		  }


		  /************************************************
		   ************************************************
		   * 	function call for CRUD operations
		   * **********************************************
		   ***********************************************/
		  
		   /**
		    * A function call that will allow you to use the Isystem
		    */
		  function processLogin(e) {

		  	e.preventDefault();	
		  	$.ajax({
	            url: url+"login",
	            type: "POST",
	            data: $("#loginDetails").serialize(),
	            dataType: "json",
	            success: function( response ) {
	                if(response.data == true){
	                	toastr.info(response.msg);
	                	setDelay(url+"dashboard")
	                }else{
	                	toastr.info(response.msg);
	                }
	            }
          	});
		  }

		  /**
		   * A function call that will exit users from system
		   */
		  function processLogout() {
		  	$.ajax({
	            url: url+"logout",
	            type: "POST",
	            data: $("#loginDetails").serialize(),
	            dataType: "json",
	            success: function( response ) {
	                if(response.data == false){
	                	toastr.info(response.msg);
	                	setDelay(url)
	                }
	            }
          	});
		  }

		  /**
		   * A function call that will create new student information in database
		   */
		  function createStudents(e) {

		  	e.preventDefault();
		  	
		  	$.ajax({
	            url: url+"create",
	            type: "POST",
	            data: $("#formCreate").serialize(),
	            dataType: "json",
	            success: function( response ) {
	                if(response.data == true){
	                	toastr.info(response.msg);
	                	setDelay(url+"dashboard")
	                }
	            }
          	});
		  }

		  /**
		   *  A function call that will update existing student information
		   */
		  function updateStudents(e) {
		  	e.preventDefault();
		  	
		  	$.ajax({
	            url: url+"update",
	            type: "POST",
	            data: $("#formUpdate").serialize(),
	            dataType: "json",
	            success: function( response ) {
	                if(response.data == true){
	                	toastr.info(response.msg);
	                	setDelay(url+"dashboard")
	                }
	            }
          	});
		  }


		  /**
		   * A function call that will remove student information in the database
		   */
		  function deleteStudents(user_id) {
		  	$.post(url+"delete/"+user_id, function(data, status){
		  		toastr.info(data.msg)
		  		setDelay(url+"dashboard")
          	});
		  }

		 
    </script>

</head>
<body>
<div class="page-header">
  <h1>Boom.Camp - Information System</h1>
</div>
<div class="container"> 

<!-- Logout Button -->
<?php 
 if($this->session->userdata('logged_in')){
 	?>
 	<a style="float:right;" href="#" onclick="processLogout();">[Exit System]</a> <br>
 	<?php 
 }
?>
```
	
</details>


<details>
<summary>   isystem/application/views/includes/footer.php </summary>

```
</div>
</body>
</html>
```

</details>


<details>
<summary>   isystem/application/views/pages/login.php </summary>

```
<h2>Enter your login credentials</h2>
<form id="loginDetails">
  <div class="form-group">
    <label for="email">Username</label>
    <input type="email" class="form-control" id="email" aria-describedby="emailHelp" placeholder="Enter email" name="username">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" class="form-control" id="password" placeholder="Password" name="password">
  </div>
  <button type="submit" class="btn btn-primary" onclick="processLogin(event);">Submit</button>
</form>
```

</details>


<details>
<summary>   isystem/application/views/pages/list.php </summary>


```
<div class="row">
    <div class="col-lg-12">                     
            <div class="pull-left">
               <a class="btn btn-primary" onclick="showCreateForm()">Add Student</a>
            </div>
     </div><br><br>
</div>
<div class="table-responsive">
<table class="table table-bordered" id="students_tbl">
  <thead>
      <tr>
          <th>Student ID</th>
          <th>Fullname</th>
          <th>Email</th>
          <th>Contact</th>
          <th>Course</th>
          <th>Action</th>
      </tr>
  </thead>
  <tbody>
   <?php foreach ($students as $student) { ?>      
      <tr>
          <td><?php echo $student->id; ?></td>
          <td><?php echo $student->fullname; ?></td>
          <td><?php echo $student->email; ?></td>   
          <td><?php echo $student->contact; ?></td>   
          <td><?php echo $student->course; ?></td>                        
      <td>
         
         <!-- Edit Action -->
         <a class="btn btn-info btn-xs" onclick="showEditForm('<?php echo $student->user_id;?>')">
          <i class="glyphicon glyphicon-pencil"></i>
         </a>

         <!-- Delete Action -->
          <button type="submit" onclick="deleteStudents('<?php echo $student->user_id;?>')" class="btn btn-danger btn-xs">
            <i class="glyphicon glyphicon-remove"></i>
          </button>

      </td>     
      </tr>
      <?php } ?>
  </tbody>
</table>
</div>



<!-- Load necessary forms -->
<?php 
$this->load->view('pages/create');
$this->load->view('pages/update');
?>
```
</details>

<details>
<summary>   isystem/application/views/pages/create.php </summary>
	
```
<form id="formCreate">
    <div class="modal fade" id="createStudents" role="dialog">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal">&times;</button>
          <h1 class="modal-title">Create Students</h1>
        </div>
        <div class="modal-body">
           <div class="form-group">
            <label for="course">Select Course</label>
            <select class="form-control" id="course" name="course">
              <?php foreach($course as $courses):?>
                <?php echo "<option value='{$courses->id}'>{$courses->name}</option>"; ?>
              <?php endforeach;?>
            </select>
          </div>
          <div class="form-group">
            <label for="username">Username</label>
            <input type="password" class="form-control" id="username" placeholder="Username" name="username">
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" class="form-control" id="password" placeholder="Password" name="password">
          </div>
          <div class="form-group">
            <label for="fullname">Fullname</label>
            <input type="fullname" class="form-control" id="fullname" placeholder="Fullname" name="fullname">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" class="form-control" id="email" placeholder="Email" name="email">
          </div>
          <div class="form-group">
            <label for="contact">Contact</label>
            <input type="contact" class="form-control" id="contact" placeholder="Contact" name="contact">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" onclick="createStudents(event)">Submit</button>
          <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        </div>
      </div> 
    </div>
  </div>
</form>
```
</details>

<details>
<summary>   isystem/application/views/pages/update.php </summary>

```
<form id="formUpdate">
    <div class="modal fade" id="updateStudents" role="dialog">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal">&times;</button>
          <h1 class="modal-title">Update Students</h1>
        </div>
        <div class="modal-body">
           <div class="form-group">
            <label for="course">Select Course</label>
            <select class="form-control" id="course_id" name="course_id">
              <?php foreach($course as $courses):?>
                <?php echo "<option value='{$courses->id}'>{$courses->name}</option>"; ?>
              <?php endforeach;?>
            </select>
          </div>
          <div class="form-group">
            <label for="username">User ID</label>
            <input type="text" readonly=true class="form-control" id="user_id" placeholder="Username" name="user_id">
          </div>
          <div class="form-group">
            <label for="username">Username</label>
            <input type="text" class="form-control" id="username" placeholder="Username" name="username">
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" class="form-control" id="password" placeholder="Password" name="password">
          </div>
          <div class="form-group">
            <label for="fullname">Fullname</label>
            <input type="text" class="form-control" id="fullname" placeholder="Fullname" name="fullname">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" class="form-control" id="email" placeholder="Email" name="email">
          </div>
          <div class="form-group">
            <label for="contact">Contact</label>
            <input type="text" class="form-control" id="contact" placeholder="Contact" name="contact">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" onclick="updateStudents(event)">Submit</button>
          <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        </div>
      </div> 
    </div>
  </div>
</form>
```

</details>

# Routes, Controllers, Models and Helpers

<details>
<summary> isystem/application/config/routes.php </summary>

```
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

$route['default_controller'] = 'Icontroller';
$route['404_override'] = '';
$route['translate_uri_dashes'] = FALSE;


$route["home"] = "Icontroller/index";
$route["login"] = "Icontroller/processLogin";
$route["logout"] = "Icontroller/processLogout";
$route["dashboard"] = "Icontroller/dashboard";
$route["create"] = "Icontroller/createStudents";
$route["get/:num"] = "Icontroller/getStudents/$1";
$route["update"] = "Icontroller/updateStudents";
$route["delete/:num"] = "Icontroller/deleteStudents/$1";
```
	
</details>



<details>
<summary>  isystem/application/controllers/Icontroller.php </summary>

```
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Icontroller extends CI_Controller {

    public function __construct() 
    {
        parent::__construct();

        //Message: Call to undefined function base_url()
        $this->load->helper('url'); 

        //Message: Call to undefined function ouput_to_json()
        $this->load->helper('isystem_helper');
        
        //load model
        $this->load->model("Imodel");

        //load session
        $this->load->library('session');

    }

    /**
     * Display login view
     */
    public function index()
    {

        $this->load->view("includes/header");
        $this->load->view("pages/login");
        $this->load->view("includes/footer");
    }


    /************************************************
    ************************************************
    *   COMPLETE THE CODE FUNCTIONALITY FROM PSEUDOCODE
    * **********************************************
    ***********************************************/

    private function checkSession()
    {
        # Documentation: https://codeigniter.com/user_guide/libraries/sessions.html?highlight=set_userdata#retrieving-session-data
        
        # Check 'logged_in' if NOT (!) present THEN redirect(base_url(), 'refresh');
    }

    /**
     * The main page that display student information
     */
    public function dashboard()
    {
        # Call function checkSession()
        $this->checkSession();

        $data['students'] = $this->Imodel->get_students();
        $data['course'] = $this->Imodel->get_course();

        $this->load->view("includes/header");
        $this->load->view("pages/list", $data);
        $this->load->view("includes/footer");
    }

    /**
     * Function that establish a session to Isystem
     */
    public function processLogin()
    {
        
        # Assign $this->input->post("username") as $username
        $username = $this->input->post("username") ?? null;

        # Assign $this->input->post("password") as $password
        $password = $this->input->post("password") ?? null;

         # IF roleExist($username,$password) and check if ($username and $password) is not equal to (!==) null THEN
         
         /**
          *
          *  $details = array(
                    'username'  => $username,
                    'password'     => $password,
                    'logged_in' => TRUE
            );

            $this->session->set_userdata($details);

            ouput_to_json([ 
                "data" => true,
                "msg" => "Login Success"
            ]);

          */
         

         # ELSE 
         
         /**
          *  ouput_to_json([ 
                "data" => false,
                "msg" => "Login failed!"
            ]);
          */
         
             
    }

    /**
     * A function that will exit you from system
     */
    public function processLogout()
    {
        # https://codeigniter.com/user_guide/libraries/sessions.html?highlight=has_userdata#adding-session-data
        
        # IF 'logged_in' has_userdata() THEN destroy all sessions 
        /**
         * ouput_to_json([ 
                "data" => false,
                "msg" => "Logout success"
            ]);
         */
    }

    /**
     * A function that will insert student details
     */
    public function createStudents()
    {

        # Call add_students($this->input->post()) 
        
        /**
         * ouput_to_json([ 
            "data" => true,
            "msg" => "Student created"
        ]);
         */
    }

    /**
     * A function that will get student details
     */
    public function getStudents()
    {

        # Assign (int)$this->uri->segment(2); as $user_id
        $user_id = (int)$this->uri->segment(2);

        # IF $user_id is_numeric
        # Call Imodel->get_student_by_id($user_id); and assign as $results THEN
        
        /**
         *  ouput_to_json([ 
                "data" => true,
                "msg" => $results
            ]);
         */
        
        # ELSE
        
        /**
         *  ouput_to_json([ 
                "data" => false,
                "msg" => "Invalid parameter for user id"
            ]);
         */
    }

    /**
     * A function that will update student details
     */
    public function updateStudents()
    {

        # Call model update_students($this->input->post()); THEN
        
        /**
         *  ouput_to_json([ 
                "data" => true,
                "msg" => "Student details updated!"
            ]);
         */
    }

    public function deleteStudents()
    {

         # Assign (int)$this->uri->segment(2); as $user_id
        $user_id = (int)$this->uri->segment(2);

         # IF $user_id is_numeric
         # Call delete_students($user_id); THEN
         
         /**
          *  ouput_to_json([ 
                "data" => true,
                "msg" => "Delete student success"
             ]);
          */
         
         # ELSE
         
         /**
          *  ouput_to_json([ 
                "data" => false,
                "msg" => "Invalid parameter for user id"
            ]);
          */
         
    }
}

```

</details>


<details>
<summary>  isystem/application/models/Imodel.php </summary>

```
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Imodel extends CI_Model{
    
    public function __construct() 
    {
        parent::__construct();

        //Load the database helper
        $this->load->database();
    }

    public function roleExist($username, $password) : bool
    {
        $this->db->where('username',$username);
        $this->db->where('password', sha1($password));
        $query = $this->db->get('users');
        return $query->num_rows() > 0 ;
    }

    public function get_course() : array
    {
        $this->db->select('id, name');
        $this->db->from('course');
        return $this->db->get()->result();
    }

    public function get_students() : array
    {
        $this->db->select('users.id as user_id, 
                           users.username as username, 
                           users.password as password, 
                           students.id, 
                           students.fullname, 
                           students.email, 
                           students.contact, 
                           course.name as course, 
                           course.id as course_id');

        $this->db->from('students');
        $this->db->join('users', 'users.id = students.user_id');
        $this->db->join('course', 'course.id = students.course_id');
        $this->db->order_by('users.id', 'ASC');
        return $this->db->get()->result();
    }

    public function get_student_by_id($user_id) : array
    {
        $this->db->select('users.id as user_id, 
                           users.username as username, 
                           users.password as password, 
                           students.id, 
                           students.fullname, 
                           students.email, 
                           students.contact, 
                           course.name as course, 
                           course.id as course_id');
        
        $this->db->from('students');
        $this->db->join('users', 'users.id = students.user_id');
        $this->db->join('course', 'course.id = students.course_id');
        $this->db->where('users.id', $user_id);
        return $this->db->get()->result();
    }



    /************************************************
    ************************************************
    *   COMPLETE THE CODEIGNITER QUERIES BELOW
    * **********************************************
    ***********************************************/

    public function add_students($post)
    {   
        # Documentation: https://codeigniter.com/userguide3/database/query_builder.html#inserting-data
        # Documentation last inserted id: https://codeigniter.com/userguide3/database/helpers.html
        
         # Set $users as array of $post['username'] and sha1($post['password'])
        $users = array(
                'username' => $post['username'],
                'password' => sha1($post['password'])
        );

        # Perform insert for 'users' table for $users array
        // QUERY HERE..

        # Assign $users as array user_id as $this->db->insert_id(), $post['course'], $post['fullname'], $post['email'] and $post['contact']
        $users = array(
                'user_id' => $this->db->insert_id(),
                'course_id' => $post['course'],
                'fullname' => $post['fullname'],
                'email' => $post['email'],
                'contact' => $post['contact']
        );

        # Perform insert query for $users array
        // QUERY HERE..
    }

    public function update_students($post)
    {    

        # Documentation : https://codeigniter.com/user_guide/database/query_builder.html#updating-data
        
        # Set $users as array of $post['username'] and sha1($post['password'])
        $users = array(
                'username' => $post['username'],
                'password' => sha1($post['password'])
        );

        # Perform update for `users` table where `id` is equal to $post['user_id']
        // QUERY HERE..

        # Set $users as array of $post['course_id'], $post['fullname'], $post['email'] and $post['contact']
        $users = array(
                'course_id' => $post['course_id'],
                'fullname' => $post['fullname'],
                'email' => $post['email'],
                'contact' => $post['contact']
        );

        # Perform update for `students` table where `user_id` is equal to $post['user_id']
        // QUERY HERE..
    }

    public function delete_students($user_id)
    {
        
        # Documentation: https://codeigniter.com/user_guide/database/query_builder.html#deleting-data
        
        # Delete users table where `id` is equal to $user_id
        // QUERY HERE..

        # Delete students table where `user_id` is equal to $user_id
        // QUERY HERE..
    }
}
?>
```

</details>


<details>
<summary>  isystem/application/helpers/isystem_helper.php </summary>

```
<?php 

function ouput_to_json($result)
{
	$CI =& get_instance();
	return $CI->output
    		  ->set_content_type('application/json') 
    		  ->set_output(json_encode($result));
}


function emptyArray($obj)
{
	if(!is_array($obj) || !is_object($obj)){
		return [];
	}

	return [];
}
```
 
</details>

# Requirements

* A way to login and logout.

* A way to CREATE new students.

* A way to UPDATE existing students.

* A way to DELETE a student.

* A way to DISPLAY lists of students.

* System should destroy all sessions.

* System should `redirect to login page` if session is NOT present.


Optional Task

* All forms should be validated.


# Finished

Submit a link of your github repository to the Google Classroom assignment related to this project.


