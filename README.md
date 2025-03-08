<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Laravel Abstract Repository</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      margin: 20px;
      max-width: 800px;
      color: #333;
    }
    h1, h2, h3 {
      color: #222;
    }
    code {
      background: #f4f4f4;
      padding: 2px 4px;
      border-radius: 4px;
      font-family: Consolas, Monaco, 'Andale Mono', 'Ubuntu Mono', monospace;
    }
    pre {
      background: #f4f4f4;
      padding: 10px;
      overflow-x: auto;
      border-radius: 4px;
    }
    ul {
      margin-left: 20px;
    }
    a {
      color: #0066cc;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <h1>Laravel Abstract Repository</h1>
  <p>
    This repository contains an abstract repository class designed for Laravel projects.
    It provides a standardized and reusable approach for performing common database operations using Laravel's Eloquent ORM.
    By following the repository pattern, this class helps separate business logic from data access, making your code cleaner and more maintainable.
  </p>
  
  <h2>Features</h2>
  <ul>
    <li><strong>CRUD Operations:</strong> Easily perform create, read, update, and delete operations.</li>
    <li><strong>Flexible Data Retrieval:</strong> Retrieve records by ID, slug, or user ID.</li>
    <li><strong>Pagination Support:</strong> Fetch collections of data with filtering and pagination.</li>
    <li><strong>Data Mapping:</strong> Standardizes the output format of individual models and collections.</li>
    <li><strong>Customizable Hooks:</strong> Override methods like <code>beforeCreate</code> to manipulate data before saving it.</li>
  </ul>
  
  <h2>Requirements</h2>
  <ul>
    <li><strong>PHP:</strong> Version 7.x or higher.</li>
    <li><strong>Laravel:</strong> Version 5.x or later (compatible with Laravel 8 and 9 as well).</li>
  </ul>
  
  <h2>Installation</h2>
  <ol>
    <li>Clone or download the repository to your local machine.</li>
    <li>Place the file in your Laravel project under the <code>App\Repositories</code> directory.</li>
    <li>Customize and extend the abstract class as needed.</li>
  </ol>
  
  <h2>Usage</h2>
  <p>
    To use this abstract repository, extend the <code>AbstractRepo</code> class in a concrete repository class and set the <code>$model</code> property to an instance of your Eloquent model.
  </p>
  
  <h3>Example: Creating a User Repository</h3>
  <pre><code>&lt;?php
namespace App\Repositories;

use App\Models\User;

class UserRepository extends AbstractRepo {

    public function __construct(User $model)
    {
        $this->model = $model;
        // Optionally, define default relationships to eager load:
        // $this->withRelations = ['profile', 'roles'];
    }
}
</code></pre>
  
  <h3>Using the Repository in Your Application</h3>
  <pre><code>// In a controller or service
$userRepo = new UserRepository(new User());

// Retrieve a user by their ID
$user = $userRepo->getByID(1);

// Retrieve a user by slug
$userBySlug = $userRepo->getBySlug('john-doe');

// Create a new user
$newUserData = [
    'name' => 'Jane Doe',
    'email' => 'jane@example.com',
    'password' => bcrypt('secret'),
];
$newUser = $userRepo->create($newUserData);

// Update an existing user
$updateData = ['name' => 'Jane Smith'];
$updatedUser = $userRepo->update(1, $updateData);

// Delete a user
$userRepo->delete(1);
</code></pre>
  
  <h2>Methods Overview</h2>
  <ul>
    <li><code>getByID($id)</code>: Retrieves a record by its primary key, including any defined relationships.</li>
    <li><code>getBySlug($slug)</code>: Fetches a record based on a slug field.</li>
    <li><code>getByUserID($user_id)</code>: Returns a record associated with a specific user ID.</li>
    <li><code>getAll($filter = [], $paginate = 10)</code>: Retrieves a paginated list of records filtered by given conditions.</li>
    <li><code>create($data)</code>: Creates a new record after optionally modifying the data with the <code>beforeCreate</code> hook.</li>
    <li><code>update($id, $data)</code>: Updates an existing record identified by its ID.</li>
    <li><code>delete($id)</code>: Deletes the record associated with the given ID.</li>
    <li><code>mapItems($items)</code>: Maps a collection of items to a standard array format.</li>
    <li><code>mapItem($item)</code>: Formats a single model instance into a standardized array structure.</li>
  </ul>
  
  <h2>Customization</h2>
  <p>
    <strong>Before Create Hook:</strong> Override the <code>beforeCreate</code> method in your child repository to manipulate or validate data before a new record is created.
  </p>
  <p>
    <strong>Mapping Functions:</strong> Customize <code>mapItem</code> and <code>mapItems</code> to change how your model data is represented in API responses or other outputs.
  </p>
  
  <h2>Contributing</h2>
  <p>
    Contributions, issues, and feature requests are welcome! Please check the <a href="#">issues page</a> to see if your feature has already been discussed or to open a new issue.
  </p>
  
  <h2>License</h2>
  <p>
    This project is open-sourced under the <a href="LICENSE">MIT License</a>.
  </p>
  
  <h2>Support</h2>
  <p>
    For further questions or support, please open an issue in the repository or contact the maintainer directly.
  </p>
  
  <p>Happy coding!</p>
</body>
</html>
