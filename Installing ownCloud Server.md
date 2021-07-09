---


---

<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
<h1 id="owncloud-quickstart-guide">ownCloud QuickStart Guide</h1>
<h2 id="introduction">Introduction</h2>
<p>This quickstart guide describes the steps to install, configure, and enable users to connect to ownCloud, a file synchronization and file sharing solution that helps to sync all your documents across various devices. The principal component in ownCloud is the ownCloud server, which can run applications on operating system platforms, such as, Linux, Windows, and Mac OS X. It can also run mobile applications for the Android and iOS operating system platforms.</p>
<h2 id="audience">Audience</h2>
<p>This section contains information for users who are interested in understanding how to create, launch, and install the ownCloud server.</p>
<h2 id="installing-the-owncloud-server">Installing the ownCloud server</h2>
<p>This section provides the steps required to launch and install the ownCloud server.<br>
You can install ownCloud in the following ways:</p>
<ul>
<li>Manual Installation</li>
<li>Sample Docker Installation</li>
<li>Sample Installation on Ubuntu</li>
<li>Linux Package Manager</li>
</ul>
<p>In the following section, the steps to install ownCloud using Ubuntu 18.04 is provided.</p>
<h4 id="prerequisites">Prerequisites</h4>
<p>This section describes the prerequisites for installing ownCloud.</p>
<ul>
<li>Ensure that an instance of Ubuntu 18.14 is installed.</li>
<li>Ensure that you are connected as the root user.</li>
</ul>
</blockquote>
<h3 id="step1-installing-apache-maria-db-and-php-on-windows">Step1: Installing Apache, Maria DB, and PHP on Windows</h3>
<p>Run the following commands to install the Apache, Maria DB, and PHP application on Windows.</p>
<pre><code>sudo apt-get install apache2
sudo apt-get install mysql-server mysql-client
sudo apt-get install php libapache2-mod-php php-mysql
php-gd php-json php-curl php-xml php-zip php.mb
sudo apt-get -y install libmcrypt-deventer code here
</code></pre>
<p>Run the following command to install another PHP extension, i.e., intl extension.</p>
<pre><code>sudo apt-get install php-intl
</code></pre>
<h3 id="step-2-download-owncloud-files-under-the-apache-directory.">Step 2: Download ownCloud files under the Apache Directory.</h3>
<p>Run the following command to download and extract the ownCloud files under the Apache directory.</p>
<pre><code>sudo -i
wget -nv https://download.owncloud.org/download/repositories/production/Ubuntu_18.04/
Release.key -O Release.key
apt-key add - &lt; Release.key
echo 'deb http://download.owncloud.org/download/repositories
/production/Ubuntu_18.04/ /' &gt; /etc/apt/sources.list.d/owncloud.list
apt-get update
apt-get install owncloud-files
</code></pre>
<h3 id="step-3-create-an-owncloud-configuration-file-for-apache.">Step 3: Create an Owncloud configuration file for Apache.</h3>
<p>Run the following command to create an ownCloud configuration file:</p>
<pre><code>nano /etc/apache2/sites-available/owncloud.conf
</code></pre>
<p>Then, add the following lines of code to point the Apache directory towards the ownCloud.</p>
<pre><code>Alias /owncloud "/var/www/owncloud/"
&lt;Directory /var/www/owncloud/&gt;
Options +FollowSymlinks
AllowOverride All
&lt;IfModule mod_dav.c&gt;
Dav off
&lt;/IfModule&gt;
SetEnv HOME /var/www/owncloud 
SetEnv HTTP_HOME /var/www/owncloud
&lt;/Directory&gt;
</code></pre>
<p>Next, press <strong>Crtl +O</strong> to write the files and then <strong>CTRL+X</strong> to save and exit.</p>
<h3 id="step-4-create-a-symlink-for-owncloud.">Step 4: Create a symlink for Owncloud.</h3>
<p>Run the following command to create a symlink for the ownCloud configuration.</p>
<pre><code>ln -s /etc/apache2/sites-available/owncloud.conf/etc/apache2/sites-enabled/owncloud.conf
</code></pre>
<h3 id="step-5-installation-of-additional-modules.">Step 5: Installation of additional modules.</h3>
<p>Add the following additional modules for ownCloud.</p>
<pre><code>ea2enmod headers
a2enmod env
a2enmod dir
a2enmod mime
a2enmod unique_id
</code></pre>
<p>After adding the additional modules, restart the Apache server using the following command:</p>
<pre><code>sudo service apache2 restart
</code></pre>
<h3 id="step-6-create-a-maria-db-database-for-owncloud.">Step 6: Create a Maria DB Database for ownCloud.</h3>
<p>Run the following commands to start and stop the MariaDB.</p>
<pre><code>sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start
</code></pre>
<p>Create a mySQL user and database for ownCloud using the following commands.</p>
<pre><code>sudo mysql
CREATE DATABASE owncloud;
</code></pre>
<p>Create a user "johndoe"and a password so that the user is assigned to the database.</p>
<pre><code>GRANT ALL ON owncloud.* to 'johndoe'@'localhost' IDENTIFIED BY 'enter_your_password';
</code></pre>
<p>Run the following command to flush privilege operations:</p>
<p><code>FLUSH PRIVILEGES;</code></p>
<p>Exit the MySQL database using the following command.</p>
<pre><code>exit
</code></pre>
<h3 id="step-7-install-setup-and-configure-the-owncloud-server.">Step 7: Install, Setup, and Configure the ownCloud Server.</h3>
<p>Open a browser and enter the following URL:</p>
<pre><code>https://owncloud.com/
</code></pre>
<p>Create an admin account on the ownCloud web page.<br>
After the admin account is created, select the <strong>storage and database</strong> option and click the MySQL/MariaDB tab.<br>
Add the MySQL details provided earlier and click <strong>Finish setup</strong> to complete the setup. As a result, the ownCloud login page appears.</p>

