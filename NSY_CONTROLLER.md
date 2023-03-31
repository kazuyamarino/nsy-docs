## NSY Controllers

### <ins>Passing variable to view</ins>
If you want to passing variable to view, you can use example below :

```
$arr = [
	'my_name' => 'Welcome',
	'mvc_page' => 'Hello',
	'date' => Carbon::now()
];

Load::template('header', $arr);
```

The above example will generate variable `$my_name`, `$date` and `$mvc_page` in the view page.

### <ins>Load MVC or HMVC view file</ins>
**Load MVC view file :**

```
Load::view(null, 'filename');
```

**Load HMVC view file :**

```
Load::view('module-name', 'filename');
```

### <ins>Sequence variable</ins>
Create a sequence of the named placeholders, e.g. `:id0`, `:id1`, `:id2`. So the code would be:

```
sequence('placeholders', 'variable')
```

**Example :**
```
$ids = [2,3,4];
$dt = sequence(":id", $ids)

print_r($dt);
```

#### Will return `print_r()` result :
```
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

### <ins>Instantiate Model class in the controller and call the method (Static Instantiate)</ins>
Instantiate the Model class in the controller is useful to make it easier for us to give variables to it.
So there is no need to rewrite the instantiate class in another method.

Just have to write it in the method, like this:

The format of `Load::model()` method :

```
Load::model(namespace_with_model, method_from_model);
```

Example for instantiate model `Hello.php` :

```
public function some_method() {
	// Instantiate Model Hello.php
	Load::model('Hello', 'mvc_page');
}
```

Example for instantiate model `Welcome.php` inside `Homepage` module :

```
public function some_method() {
	// Instantiate Model Welcome.php
	Load::model('Homepage\Welcome', 'hmvc_page');
}
```

### <ins>Instantiate Model class in the controller and call the method (Manual Instantiate)</ins>

Example for instantiate model `Hello.php` :

```
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

Example for instantiate model `Welcome.php` inside `Homepage` module :
```
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