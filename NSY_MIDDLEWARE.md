# The Middlewares
NSY has support middleware, which is the process of filtering a process before it is run by the controller by NSY.

NSY uses Onion Library from https://github.com/esbenp/onion. A standalone middleware library without dependencies inspired by middleware in Laravel (Illuminate/Pipeline).

NSY has 2 middleware modes, namely before and after.
* Before, as a middleware that runs before the core process.
* After, as middleware that runs after the core process.

NSY provides middleware support from the Routing side.

**For example :**

Contents of the `Web.php` route file
```
Route::get('/', function() {
	$middleware = [
		new BeforeLayer(),
		new AfterLayer()
	];

	Route::middleware($middleware)->for('Welcome@index');
});
```

Contents of the `AfterLayer.php` file.
```
public function peel($object, \Closure $next)
{
	$response = $next($object);

	/*
	Result from after middleware here.
	*/
	$object = 'After Core';
}
```

Contents of the `BeforeLayer.php` file
```
public function peel($object, \Closure $next)
{
	$condition = 1;

	if ( $condition == 1 ) {
		/*
		Response if condition true,
		Result from before middleware here.
		*/
		$object = 'Before Core';

		$response = $next($object);
		} else {
			/*
			Response if condition false.
			*/
			$object = 'Middleware : Access controller canceled';

			exit();
		}
}
```
