# NSY Controllers

## Passing variable to view

If you want to passing variable from Controller to View, you can use example below :

```php
$arr = [
 'my_name' => 'Welcome',
 'mvc_page' => 'Hello',
 'date' => Carbon::now()
];

Load::template('header', $arr);
```

The above example will generate variable `$my_name`, `$date` and `$mvc_page` in the View page.

## Load MVC or HMVC view file

To display the View page from the Controller.

**Load MVC view file :**

```php
Load::view(null, 'filename');
```

Displays the View `index.php` from the Controller, example :

```php
Load::view(null, 'index');
```

**Load HMVC view file :**

```php
Load::view('module-name', 'filename');
```

Displays the View `index.php` page in the `Login` module, example :

```php
Load::view('Login', 'index');
```

## Sequence variable

Create a sequence of the named placeholders, e.g. `:id0`, `:id1`, `:id2`. So the code would be:

```php
sequence('placeholders', 'variable')
```

**Example :**

```php
$ids = [2,3,4];
$dt = sequence(":id", $ids)

print_r($dt);
```

Will return `print_r()` result :

```php
Array
(
   [0] => :id0,:id1,:id2
   [1] => Array
       (
           [:id0] => 2
           [:id1] => 3
           [:id2] => 4
       )
)
```

## Instantiate Model class in the controller & call the method (Static Instantiate)

Instantiate the Model class in the controller is useful to make it easier for us to give variables to it.
So there is no need to rewrite the instantiate class in another method.

Just have to write it in the method, like this:

The format of `Load::model()` method :

```php
Load::model(namespace_with_model::class)->method_from_model();
```

Example for instantiate class `Hello.php` :

```php
use System\Models\Hello;

public function some_method() {
 // Instantiate Model Hello.php
 Load::model(Hello::class)->mvc_page();
}
```

Alternatively, you can write this :

```php
public function some_method() {
 // Instantiate Model Hello.php
 Load::model(System\Models\Hello::class)->mvc_page();
}
```

Example for instantiate class `Welcome.php` inside `Homepage` module :

```php
use System\Modules\Homepage\Models\Welcome;

public function some_method() {
 // Instantiate Model Welcome.php
 Load::model(Welcome::class)->hmvc_page()
}
```

Or this :

```php
public function some_method() {
 // Instantiate Model Welcome.php
 Load::model(System\Modules\Homepage\Models\Welcome::class)->hmvc_page()
}
```

## Instantiate Model class in the controller and call the method (Common Instantiate)

Example for instantiate class `Hello.php` :

```php
use System\Models\Model_Welcome;

public $m_hello;

public function __contruct() {
 // Instantiate Model Hello.php
 $this->m_hello = new Hello;
}

public function yours() {
 $this->m_hello->mvc_page();
}
```

Example for instantiate class `Welcome.php` inside `Homepage` module :

```php
use System\Modules\Homepage\Models\Model_Welcome;

public $m_welcome;

public function __contruct() {
 // Instantiate Model Welcome.php
 $this->m_welcome = new Welcome;
}

public function yours() {
 $this->m_welcome->hmvc_page();
}
```
