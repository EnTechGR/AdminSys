connect
-------

To communicate over a network, a computer must have an IP address.

The computer can choose its own IP address (**static**) or can ask a DHCP server to assign one (**dynamic**).

Generally, clients (smartphones, laptops, etc.) rely on DHCP servers to have a dynamic IP address, while servers typically have a static IP address.

For this project, you will need to add these 3 VMs:

### For VirtualBox

*   [01\_connect\_box](https://assets.01-edu.org/sys/01_connect_box.tar.gz)
    
*   [01\_connect\_machine1](https://assets.01-edu.org/sys/01_connect_machine1.tar.gz)
    
*   [01\_connect\_machine2](https://assets.01-edu.org/sys/01_connect_machine2.tar.gz)
    

### For UTM

*   [01\_connect\_box](https://assets.01-edu.org/sys/01_connect_box.utm.zip)
    
*   [01\_connect\_machine1](https://assets.01-edu.org/sys/01_connect_machine1.utm.zip)
    
*   [01\_connect\_machine2](https://assets.01-edu.org/sys/01_connect_machine2.utm.zip)
    

### Network Configuration

The VMs are configured according to this diagram:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML        `N E T W O R K S                C O M P U T E R S  _______________________________     ________________________  .-----------------------------.  |           Internet          |  '-----------------------------'                 ^                 |                 v  .-----------------------------.  |            NAT              |  |                             |  |         DHCP server         |     .----------------------.  |          DNS server         |     |         box          |  |                             |     |                      |  |       (10.0.2.2) NIC        |<--->|  INT_2 (10.0.2.15)   |  |                             |     |   ^                  |  '-----------------------------'     |   |                  |  .-----------------------------.     |   |                  |  |       Internal Network      |     |   | DHCP server      |  |                             |     |   v                  |  |                           |<----->|  INT_1 (192.168.0.1) |  |                           | |     |                      |  |                           | |     '----------------------'  |                           | |     .----------------------.  |                           | |     |       machine1       |  |                           | |     |                      |  |                           |<----->|  INT_1 (192.168.0.2) |  |                           | |     |                      |  |                           | |     '----------------------'  |                           | |     .----------------------.  |                           | |     |       machine2       |  |                           | |     |                      |  |                           |<----->|  INT_1 (192.168.0.2) |  |                             |     |                      |  '-----------------------------'     '----------------------'`

> **Note:** You only have control over machine2. This computer has Internet access through the box.**Credentials:** Login: root | Password: (a single space).

The Problem
-----------

Initially, machine1 and machine2 share the same IP address (192.168.0.2), causing an IP conflict. You can observe the resulting packet loss (likely >10%) by running:

Bash

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   timeout --signal SIGINT 1m ping google.com   `

Solutions
---------

### 1\. Change the IP address to avoid the conflict (Static)

To temporarily resolve the conflict by manually assigning a unique static IP (e.g., 192.168.0.3) to machine2:

1.  Baship addr del 192.168.0.2/24 dev enp0s3
    
2.  Baship addr add 192.168.0.3/24 dev enp0s3
    

### 2\. Make the IP address dynamic (DHCP)

To let the box (acting as a DHCP server) automatically assign a valid IP address to machine2:

1.  Baship addr flush dev enp0s3
    
2.  Bashdhclient enp0s3
    
3.  Baship addr show enp0s3
    

After running dhclient, the IP conflict is resolved automatically by the server, and your connectivity to google.com should stabilize with 0% packet loss.