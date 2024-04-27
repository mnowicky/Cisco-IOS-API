# Cisco-IOS-API
An API for interacting with Cisco (IOS, NX-OS, IOS-XR) based devices. 

This API is currently under development to further normalize and optimize it's functions; as it was created to meet my own needs in working with ciso networks.

Files:
 - ciscoAPI.py - The module containing the API's main class and the focus of this repo. 
 - config.yml - A basic config file to use with this api. Contains basic information for connecting, configuration details for specific tasks, as well as plaintext credentials for login. Under credentials, list out every possible usename and password combination that might be needed to login to any of the devices you will be working with. 
 - logger.py - A simple logger, used within many of the API's functions. You can replace this with your own logger, or use built-in logging if you like. 

General Usage:
This API is intended to be used to help automate configuration tasks for Cisco devices. Use it to create your own projects. Simplifies connecting to cisco devices and issuing configuration commands or retrieving specific information to be utilized in your own programs or functions. 

1) Connecting:
   Import config file; use [connection] and [credentials] from config file to pass to the connectSwitch function from the API class to obtain a connection object. Pass connection object as an argument to subsequent functions offered by the api.

   ex. usage:

   ```python
   from ciscoAPI import Cisco as cisco
   import yaml
   
   #
   with open('config.yml', 'r') as configFile:
     config = yaml.safe_load(configFile)

   def run()
     creds = config['credentials']
     ip = config['connection']['switch_ip']
     config.close()

     #connect using connectSwitch() function from API
     connection = cisco.connectSwitch(ip, creds)

     #pass connection object to be used with other api functions
     vlan = 10
     cisco.set_voice_vlans(connection, vlan)

     #retrieve information to be passed to another function
     interfaceStatus = cisco.return_int_status(connection)
     for int in interfaceStatus:
       cisco.enable_interface(int)

   if __name__ == "__main__":
     run()
