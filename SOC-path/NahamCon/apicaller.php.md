
```shell
curl http://challenge.nahamcon.com:32542/ | grep -iE 'flag|admin|api|debug|<!--' % Total % Received % Xferd Average Speed Time Time Time Current Dload Upload Total Spent Left Speed 100 5589 100 5589 0 0 4510 
<!-- note: should not be accessable --> 
0 0:00 <!-- <a href="/test" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">Test</a> --> :01 0:00:0 <!-- Mobile menu --> 1 --:- <!-- note: should not be accessable --> 
<?php 
	class APICaller { 
	private $url = 'http://localhost/api/'; 
	private $path_tmp = '/tmp/';
	private $id;
	public function __construct($id, $path_tmp = '/tmp/') { 
		$this->id = $id; 
		$this->path_tmp = $path_tmp; 
	} 
	public function __call($apiMethod, $data = array()) { 
		$url = $this->url . $apiMethod; $data['id'] = $this->id; 
		foreach ($data as $k => &$v) { 
			if ( ($v) && (is_string($v)) && str_starts_with($v, '@') ) { 
				$file = substr($v, 1); 
				if ( str_starts_with($file, $this->path_tmp) ) { 
					$v = file_get_contents($file); 
				} 
			} 
			if (is_array($v) || is_object($v)) { 
				$v = json_encode($v); 
			} 
		} // Call the API server using the given configuraions 
		$ch = curl_init($url); 
		curl_setopt_array($ch, array( CURLOPT_POST => true, CURLOPT_POSTFIELDS => $data, CURLOPT_RETURNTRANSFER => true, CURLOPT_HTTPHEADER => array('Accept: application/json'), )); 
		$response = curl_exec($ch); 
		$error = curl_error($ch); 
		curl_close($ch); 
		if (!empty($error)) { 
		throw new Exception($error); 
	} return $response; 
} 
} -:-- 45 <!-- <a href="/test" class="block rounded-md px-3 py-2 text-base font-medium text-gray-300 hover:bg-gray-700 hover:text-white">Test</a> --> 10 <h1 class="capitalize mb-4 text-4xl font-extrabold leading-none tracking-tight text-gray-600 md:text-5xl lg:text-6xl "> API manager <p class="mb-6 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48">Manage API calls, methods and extract data</p>

```