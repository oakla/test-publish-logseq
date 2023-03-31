- [[Pip]]
	- Setup in the CBA environment:
		- Within the CBA IT infrastructure, pypi packages can be accessed at `https://secret-place`. To tell Pip to get packages from this location, you have two choices.
		- 1. Use flags on the command line:
		  ``` sh
		  $ python -m pip install --user --force-reinstall --no-cache-dir --trusted-host artifactory.ai.cba --index-url secret <package-name>
		  ```
		-
		- 2. Use a config for a persistent solution.
			- Create a `pip.ini` file at `%appdata%\pip` containing the following
			  ``` ini
			  [global]
			  index-url = https://secret
			  trusted-host = secret
			  ```
			- Then run Pip as normal:
			  ``` sh
			  $ python -m pip install <package-name>
			  ```
			- Original [source here](https://stackoverflow.com/a/43473312).
			- `pip.ini` [documentation here](https://pip.pypa.io/en/stable/user_guide/#config-file)
- [[Requests]]
	- To make REST requests in Python (e.g. `requests.get(...)`), you might need to set the `verify` and `proxies` parameters as follows:
	- ``` pythimport requests
	  
	  url = "some.place"
	  cert = r"secret-place"
	  proxies = {
	      "http": "proxy-secret",
	      "https": "proxy-secret"
	  }
	  
	  r = requests.get(url, verify=CERT_PATH, proxies=proxies)
	  s)
	  ```
	  An alternative to using CERT_PATH is to set verify to `False`. This is acceptable in one-off scenarios, but may not be secure as an ongoing practice. See [this Stack Overflow answer](https://stackoverflow.com/a/12864892)
-
- [[Known Issues]]
	- **numpy-1.24.2 on CBA VDI should be avoided**. If Numpy version 1.24.2 is installed from the CBA pypi index, Python will crash when importing numpy
-