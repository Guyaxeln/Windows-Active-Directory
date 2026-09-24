# 🌐 IIS Web Server Configuration

## 🗒️ Overview
In this section of my Active Directory lab, I installed and configured Internet Information Services (IIS) on **Windows Server 2022** (`DC01.itech.local`, `192.168.56.10`) to demonstrate how to set up and host internal web services in an enterprise environment. The lab also involved testing connectivity and accessibility from a domain-joined **Windows 10** client (`PC-01`, `192.168.56.102`). This setup illustrates basic web server deployment, custom site creation, DNS name resolution, and internal network publishing within the `itech.local` domain.

## 🛠️ Configuration Steps

### 1. ⬇️ Install the IIS Role
Using **Server Manager** on `DC01.itech.local`, I launched the **Add Roles and Features Wizard**:

- Selected **Role-based or feature-based installation**
- Chose `DC01.itech.local` as the destination server
- Selected the **Web Server (IIS)** role and accepted the required management tools (**IIS Management Console**)
- Completed the wizard and confirmed the installation finished successfully, including core components such as Common HTTP Features, Health and Diagnostics, and HTTP Logging

![Add Roles and Features Wizard - Before You Begin](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/01-before-you-begin.png)
![Selecting Role-based or feature-based Installation](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/02-installation-type.png)
![Selecting DC01.itech.local as the Destination Server](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/03-destination-server.png)
![Selecting the Web Server (IIS) Role and Adding Management Tools](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/04-select-server-roles.png)
![Web Server Role (IIS) Overview](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/05-web-server-role-overview.png)
![Installation Progress and Results](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/06-installation-progress.png)

### 2. ✅ Confirm Installation and Test Default Website
After installation completed, I opened a browser on the server and navigated to `http://localhost`, confirming the IIS default welcome page loaded successfully.

![IIS Default Page in Browser (localhost)](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/07-iis-default-page-localhost.png)

### 3. 🌐 Configure a Custom Website and DNS Record
To publish a custom internal page:

- Edited the site's `index.html` to display a custom page titled **"Welcome to my Testing Page"**, including an About section and a Contact section
- Opened **DNS Manager** on the domain controller and added a **Host (A)** record named `www` in the `itech.local` forward lookup zone, pointing to `192.168.56.10`
- Verified other domain records were already present, including `dc01` and the client record `PC-01` (`192.168.56.102`)
- Browsed to `http://www.itech.local` and confirmed the custom page rendered correctly

![DNS Manager - www Host (A) Record Added in itech.local Zone](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/12-dns-manager-www-record.png)
![Custom Page Displayed at www.itech.local](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/13-custom-page-www-itech-local.png)

### 4. 🚀 Create an Additional Site in IIS
To demonstrate hosting more than one site on the same server, I added a second website:

- Opened **IIS Manager → Sites → Add Website**
- Site name: `testing.local`
- Physical path: `C:\inetpub\wwwroot\Testing`
- Binding: `http`, Port: `8080`
- Confirmed the new site appeared alongside the Default Web Site and started successfully

![IIS Manager - Adding a New Website (testing.local)](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/08-iis-manager-add-website.png)
![Setting Physical Path](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/09-add-website-browse-folder.png)
![Setting Port Binding (8080)](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/10-add-website-binding-8080.png)
![Sites List Showing Default Web Site and testing.local](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/11-sites-list-testing-local.png)

### 5. 📶 Verify Access from a Domain-Joined Client
From the domain-joined Windows 10 client (`PC-01`), I opened a browser and navigated to `http://www.itech.local`. The custom page loaded successfully, confirming DNS resolution and LAN accessibility from a client machine.

![Custom Web Page Displayed in Browser on PC-01](https://github.com/Guyaxeln/Windows-Active-Directory/blob/main/Webserver%20Configuration/14-custom-page-client-pc01.png)

## 📝 Summary
In this lab, I successfully installed and configured IIS on Windows Server 2022, published a custom web page resolved through an internal DNS record, created a secondary site bound to a custom port, and verified access from a domain-joined Windows 10 client. This exercise demonstrates my ability to:

- Deploy and configure web services in a Windows Server environment
- Manage IIS sites, bindings, and physical paths
- Create and manage internal DNS records to support name resolution
- Test and validate network connectivity across Active Directory-joined endpoints
