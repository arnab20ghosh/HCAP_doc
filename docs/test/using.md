---
title: Run tests
---
# Run tests
Hitachi Cloud Accelerator Platform - Test (Test Accelerator) is a Continuous Testing (CT) platform that increases the delivery speed from Development to QA to Operations, while adopting DevOps best practices. Test Accelerator enables you to test your web applications with a wide range of browsers and provides state-of-the-art test result data analytics.<br>

This topic describes how you can use Test Accelerator to run different types of tests on your web application, run infrastructure and scale tests, view test results, and schedule test jobs.

## <a id="content" name="content"></a>Contents

Get started

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'overview'})" style="text-decoration:none">Overview of tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'access'})" style="text-decoration:none">Accessing Test Accelerator</a>

Run tests

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'custom-automated'})" style="text-decoration:none">Customizing your automation code</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'url'})" style="text-decoration:none">Running URL tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'manual'})" style="text-decoration:none">Running manual tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'security'})" style="text-decoration:none">Running security tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'api'})" style="text-decoration:none">Running API tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'automated'})" style="text-decoration:none">Running automated tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'load'})" style="text-decoration:none">Running scale tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra'})" style="text-decoration:none">Running infrastructure tests</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'codeless'})" style="text-decoration:none">Running codeless infrastructure tests</a>

View test results

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">Viewing and downloading test results</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'logs'})" style="text-decoration:none">Viewing and downloading logs</a>

Manage test jobs

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'jobs-list'})" style="text-decoration:none">Viewing jobs list</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'stop'})" style="text-decoration:none">Stopping test jobs</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'rerun'})" style="text-decoration:none">Rerunning test jobs</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'schedule-list'})" style="text-decoration:none">Managing job schedules</a>

## <a id="overview" name="overview"></a>Overview of tests

Test Accelerator provides the ability to automate the creation of test setups and perform different types of tests on your web application. This enables you to concentrate on the actual use cases of your application and reduce the time required to deliver the application.

Test Accelerator enables you to perform the following different types of tests:

- **URL test** -- This test can instantly check the availability of a web application on different browsers.
- **Security test** -- This test performs a security check of your web application by running different types of security packs on the application.
- **API test** -- This test covers the testing of the application programming interfaces (APIs) of your applications to determine if they meet the functionality, reliability, performance, and security expectations.
- **Automated (Cross Browser) test** -- This test automatically provisions machines with browsers of your choice and then runs your existing automation test suites in the selected browsers. 
- **Scale test** -- This test performs the scale testing of your web application across a range of browsers. It enables you to configure multiple browsers, the browser count to test the load, the automation test suite, and the run time in hours.
- **Manual test** -- This test quickly provisions Kubernetes pods with the selected browsers and reduces the effort to create test setups. You can concentrate on testing the actual use cases.
- **Infrastructure test** -- This test covers the testing of your IT infrastructure, such as servers, network switches, and routers. Test Accelerator supports the Serverspec, Inspec, Azure Spec, AWS Spec, and GCP Spec specification types.
- **Codeless Infra test** -- This test covers the testing of your AWS, Azure, or Google Cloud Platform (GCP) resources by using the default spec code that is provided by Test Accelerator. It saves time and resources spent on writing your own custom code.

_**Note:** The URL, manual, security, and codeless infra tests do not have a dependency on any automation test suite._

## <a id="access" name="access"></a>Accessing Test Accelerator

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'logon'})" style="text-decoration:none">Sign in to Hitachi Cloud Accelerator Platform</a>.

   For information about creating a Cloud Accelerator Platform account, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'create'})" style="text-decoration:none">Create & access account</a>.

2. Click the **Accelerator** icon (![](/images/rean-platform-common/icon_accelerator.PNG)) in the top-left corner.

3. From the list of accelerators, select **Hitachi Cloud Accelerator - Test**.

   The Home page of Test Accelerator appears.

_**Note:** You can access Test Accelerator and perform various actions only if your Cloud Accelerator Platform administrator has granted you the appropriate permissions._

## <a id="custom-automated" name="custom-automated"></a>Customizing your automation code

Before you run the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'automated'})" style="text-decoration:none">automated (cross-browser) tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'load'})" style="text-decoration:none">scale (load) tests</a>, or <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'api'})" style="text-decoration:none">API tests</a> with your own automation code, perform the following procedures to customize your automation code:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'browser-support'})" style="text-decoration:none">Configure environment variables in your automation code</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'unique-data'})" style="text-decoration:none">Configure the use of unique data for each test run</a>

### <a id="browser-support" name="browser-support"></a>Configure environment variables in your automation code

To use Test Accelerator effectively, you must customize your automation code to use the environment variables that are exposed by Test Accelerator. Using these environment variables makes your automation code URL- and browser-independent and enables it to run on any environment without requiring changes to your code.

- **BROWSER**

  This environment variable enables you to run your automation code on the browsers that are selected while creating automated (cross-browser) or scale test jobs in Test Accelerator.<br>

  When the automated (cross-browser) or scale test job starts, the **Browsers** field value is exposed as the **BROWSER** environment variable, as shown below:

  ```
  BROWSER=firefox
  BROWSER=chrome
  ```
  
  To configure the browsers correctly, you must use this environment variable in your automation code, as shown in the following Java code example: 
  
  ```
  browser = System.getenv(Constants.BROWSER);
  ```
  
- **TEST_URL** 

  Each web application has a URL on which the automated (cross browser), scale test, or API test is run. This URL can change with time, environment, and many other factors. Each time the URL changes, you also need to update your automation code.<br>

  This environment variables enables you to run your automation code on the web application URL that is provided while creating automated (cross-browser), scale test, or API test jobs in Test Accelerator.<br>

  When the automated (cross-browser), scale test, or API test job starts, the **Application URL** field value is exposed as the **TEST_URL** environment variable, as shown below:

  ```
  TEST_URL=http://domain-name.com
  ```

  To configure the web application URL correctly, you must use this environment variable in your automation code, as shown in the following Java code example:

  ```
  test_url = System.getenv(Constants.TEST_URL);
  ```

  Using the **TEST_URL** environment variable makes your automation code URL-independent and enables it to run on any environment without requiring any changes to your code.

_**Note:** If you do not configure web drivers correctly, your tests might fail and you might not be able to use all features of Test Accelerator._

### <a id= "unique-data" name="unique-data"></a>Configure the use of unique data for each test run

In the case of automated (cross-browser) or scale tests, if you choose to run your automation code on multiple browsers, either sequentially or in parallel, you might want to use unique data for each execution. Test Accelerator exposes the **RUN_INDEX** environment variable, which has a unique incremental value for each browser.<br>

For example, if you are running tests on five browsers in parallel, the **RUN_INDEX** environment variable increments from 0 to 4 respectively for each browser:

```
RUN_INDEX=0     # Browser 1
RUN_INDEX=1     # Browser 2
RUN_INDEX=2     # Browser 3
...
...
...
RUN_INDEX=n-1   # Browser n
```

The following table lists a few scenarios in which you might need to use unique data for each execution. The table also describes how the **RUN_INDEX** variable might provide a solution in these scenarios.

| Scenario                                                     | Possible solution                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Use a different login credential set for each execution when running 10 browsers in parallel | Maintain a CSV file of multiple user-password pairs and use the **RUN_INDEX** value to fetch unique rows of credential pairs for each instance of your browser. |
| Select a different drop-down value for each execution        | Pass the **RUN_INDEX** value to the Select Drop-down method, which in turn selects a value based on the drop-down index. |
| Buy a unique product for every execution on an e-commerce website | Use the **RUN_INDEX** value as the locator index to buy different products in every instance of the browser. |

## <a id="url" name="url"></a>Running URL tests 

The URL test enables you to quickly test the availability of a web application by testing URL access to that application across various browsers. You must provide the application URL and the text that Test Accelerator must search for on the Home page of that application. The test passes only if Test Accelerator finds that text on the Home page.

1. On the Home page, click **New Test**.

2. In the Select Test window, click **URL Test**.

   The URL Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_urltest.PNG)

3. Under **Select Browser**, click the browser on which you want to run the URL test and then select the appropriate versions.

   Repeat this step for each browser on which you want to run the URL test.

4. In **Job Name**, enter a unique name for your test job.

5. In **Application URL**, enter the Home page of the web application whose availability you want to test.

6. In **Search Text**, enter the text that Test Accelerator must search for on the Home page of the web application.

   Test Accelerator considers the URL test to be successful if this specified text is available on the page.

7. In **Timeout (secs)**, define the duration, in seconds, for which Test Accelerator should wait to access the URL.  

8. _(Optional)_ To check all the links that are available on the specified page, select **Crawl URL**.

9. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

10. Click **SUBMIT**.

    The tests in Test Accelerator run on Kubernetes cluster. Test Accelerator creates separate Kubernetes pods using a Kubernetes job to run the test in parallel on all selected browsers.

11. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="manual" name="manual"></a>Running manual tests

While automation testing significantly reduces the time and effort required to test a web application, you might still need to run manual tests for a few specific scenarios. Also, if an automated test fails for any browser, you might need to create a setup with that browser and then manually run the tests.<br>

The Manual test enables you to quickly launch a Kubernetes pod with the appropriate browser version. 

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Manual**.

   The Manual Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_manualtest.PNG)

3. Under **Select Browser (s)**, click the browser on which you want to run the manual test and select appropriate versions. 

   Repeat this step for each browser on which you want to run the manual test. You can select multiple versions for each browser.

4. In **Name**, enter a unique name for your test job.

5. Click **SUBMIT**. 
   
   A Kubernetes job is launched for each browser version for running the manual test. 
   
6. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="security" name="security"></a>Running security tests

The Security test enables you to perform a security check of your web application by running different types of security packs on the application. You can also view a detailed analysis of the test packs that are run on the web application. You can also enter the security credentials required for logging into your web application, if the web application requires a login.  

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Security**.

   The Security Test page appears, as shown in the following image.

   ![rt_securitytest.PNG](/images/rean-test/rt_securitytest.PNG)

3. In **Job Name**, enter a unique name for your test job.

4. In **Application URL**, enter the URL on which you want to run the security test.

5. In **Spider-Depth**, enter the depth of the spider crawl.

6. Select **Use Ajax Spider**, to use the Ajax spider add-on.

7. Select **Login**, to enter the user credentials for the application you want to test. To use the **Login** feature, make sure that the credentials tab (username and password), and the login button are on the same page. 

   ![](/images/rean-test/loginsecurity.png)

   a.  Enter **Username** and **Password** for the web application. 

   b.  In the **Enter login field and button details field**, enter the following parameters:

   - **username_field_xpath**: The xpath for the username field on the web application page.
   - **password_field_xpath**: The xpath for the password field on the web application page.
   - **submit_button_xpath**: The xpath for the submit button on the web application page.
   - **login_url**: The URL for logging in to the the web application page.
   - **logout_url**: The URL for logging out of the the web application page.

8. Under **Select security Packs**, select the appropriate check boxes:

   - **App Scan** -- This security pack runs automated application-level tests against the web application using OWASP Zed Attack Proxy (ZAP).
   - **Http Header** -- This security pack verifies that HTTP headers adequately protect data from attackers.

9. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

10. Click **SUBMIT**.

11. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="api" name="api"></a>Running API tests

The API test covers the testing of the application programming interfaces (APIs) of your applications to determine if they meet the functionality, reliability, performance, and security expectations.

1. (*Optional*) <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'custom-automated'})" style="text-decoration:none">Customize your automation code</a> to use the TEST_URL environment variable that is exposed by Test Accelerator.

2. On the Home page, click **New Test**.

3. In the Select Test window, click **API**.

   The API Test page appears, as shown in the following image.

   ![](/images/rean-test/API1.PNG)

4. In the **BASICS** step, perform the following actions:

   - In **Job Name**, enter a unique name for your test job.
   - In **Application URL**, enter the API URL of the web application for testing.
   - Click **Next**.

5. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*

   - Click **NEXT**.

6. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the automation test suite.

   - In **Test Run Command**, enter the command for running the automation test suite.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the automation test suite.

   - In **Output Directory**, specify the path to the Output directory where reports are generated after running your automation code. This path must be relative to the automation code directory.

     You can see the contents of this directory by clicking the bubble that is created for the browser.

   - In **Report File**, specify the path of the file that has information about the test execution. This file path must be relative to the Output directory that you have specified.

     Test Accelerator uses this file to analyze the test results and generate a consolidated report. Test Accelerator supports the report file that is generated by some standard tools such as JUnit, Cucumber, and UFT. If Test Accelerator is not able to parse the report that the automation code generates, you must write code to parse the report file and generate the data that Test Accelerator supports.

7. In the right panel, verify that the details you have specified are correct.

8. To run this test job multiple times based on a configured schedule, click **SCHEDULE**. For information about scheduling tests, see [Scheduling test jobs](https://reanplatform-help.reancloud.com/#/rean-platform-docs/accelerator?viewAccelerator=rean-test&viewPage=run-tests&viewSection=scheduled-job).

9. Click **SUBMIT**.

10. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="automated" name="automated"></a>Running automated tests

The cross-browsers automated test covers the complete automation testing of your web application across a range of browsers. Test Accelerator supports the Selenium automation tool.<br>

You can select browsers and specify your test cases from a GitHub repository or upload a ZIP file. Test Accelerator runs all your test cases against the web application on all selected browsers. Cross-browser testing significantly reduces the effort to create the setups and overall testing, allowing you to concentrate on the actual use case.<br>

### <a id="run-automated" name="run-automated"></a>Run an automated test with custom code

1. (*Optional*) <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'custom-automated'})" style="text-decoration:none">Customize your automation code</a> to use the environment variables that are exposed by Test Accelerator.

2. On the Home page, click **New Test**.

3. In the Select Test window, click **Cross Browser**.

   The Automated Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_automate.PNG)

   The procedure to configure an automated test consists of three steps – select the browsers, provide the codebase, and define execution details.

4. In the **BASICS** step, perform the following actions:

   - Under **Select Browser(s)**, click the browser on which you want to run the test suite and select the appropriate versions. 

     Repeat this step for each browser on which you want to run the automated test suite.

   - In **Job Name**, enter a unique name for your automation job.

   - In **Application URL**, enter the application URL on which Test Accelerator must run the automation test suite.

   - Click **NEXT**.

5. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*

   - Click **NEXT**.

6. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the automation test suite.

   - In **Test Run Command**, enter the command for running the automation test suite.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the automation test suite.

   - In **Output Directory**, specify the path to the Output directory where reports are generated after running your automation code. This path must be relative to the automation code directory.

     You can see the contents of this directory by clicking the bubble that is created for the browser.

   - In **Report File**, specify the path of the file that has information about the test execution. This file path must be relative to the Output directory that you have specified. 

     Test Accelerator uses this file to analyze the test results and generate a consolidated report. Test Accelerator supports the report file that is generated by some standard tools such as JUnit, Cucumber, and UFT. If Test Accelerator is not able to parse the report that the automation code generates, you must write code to parse the report file and generate the data that Test Accelerator supports.

7. In the right panel, verify that the details you have specified are correct.

   ![](/images/rean-test/rt_automatedsummary.PNG)

8. _(Optional)_  To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

9. Click **SUBMIT**.

   Test Accelerator provisions the selected browser versions, downloads and runs your automation test suite, and captures screenshots for each test that is run. 

10. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="load" name="load"></a>Running scale tests

The ScaleNow test covers the scale testing of your web application across a range of browsers. You can select multiple browsers and their versions, the browser count to test the load, the automation test suite, and the run time in hours. ScaleNow significantly reduces your effort to create setups and simultaneously test on multiple machines, enabling you to concentrate on the actual use case.<br>

Test Accelerator runs all your test cases against your web application on all the selected browsers simultaneously and for the specified time. The ScaleNow test also has an incremental load feature that enables you to add users incrementally and create a real-time scenario for load testing. A new test job is created for each incremental load.<br>

**To scale test your web application, perform the following actions:**

1. (*Optional*) <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'custom-automated'})" style="text-decoration:none">Customize your automation code</a> to use the environment variables that are exposed by Test Accelerator.

2. On the Home page, click **New Test**.

3. In the Select Test window, click **Scale Now**.

   The procedure to configure a scale test consists of three steps – select the browsers, provide the codebase, and define execution details.

4. On the ScaleNow page, in the **BASICS** step, perform the following actions:

   - Under **Select Browser(s)**, click the browser on which you want to run the test suite and select the appropriate versions.

     Repeat this step for each browser on which you want to run the automation test suite. You can select multiple versions of each browser.

   - In **Job Name**, enter a unique name for your test job.

   - In **Application URL**, enter the application URL on which Test Accelerator must run the automation test suite.

   - In **Parallel Users Count**, select the number of browsers that Test Accelerator must create in parallel to put load on your web application.

   - In **Hours to Run**, select the duration, in hours, for which the test suite must run continuously and in the repeat mode. 

   - _(Optional)_ To incrementally increase the users that Test Accelerator creates to put load on your web application, select **Incremental Load**.

     If you select this check box, you must also perform the following actions:

     - In **Increase Users with**, enter the number of users that Test Accelerator must create in parallel after the specified interval.
     - In **Interval (min)**, enter the duration, in minutes, after which Test Accelerator must create the specified number of users.

   - Click **NEXT**.
   
5. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*

     - Click **NEXT**.

6. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the automation test suite.

   - In **Test Run Command**, enter the command for running the automation test suite.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the automation test suite.

   - In **Output Directory**, specify the path to the Output directory where reports are generated after running your automation code. This path must be relative to the automation code directory.

     You can see the contents of this directory by clicking the bubble that is created for the browser.

   - In **Report File**, specify the path of the file that has information about the test execution. This file path must be relative to the Output directory that you have specified. 

     Test Accelerator uses this file to analyze the test result and generate a consolidated report. Test Accelerator supports the report file that is generated by some standard tools such as JUnit, Cucumber, and UFT.

7. In the right panel, verify that the details you have specified are correct.

   ![](/images/rean-test/rt_scalenow.PNG)

8. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

9. Click **SUBMIT**. 

   Test Accelerator provisions the selected browsers on Kubernetes pods, downloads and runs your automation test suite. 

10. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="infra" name="infra"></a>Running infrastructure tests

The infrastructure test covers the testing of your IT infrastructure, such as servers, network switches, routers, and firewalls. Test Accelerator supports the specification types listed in the following table.

| Specification type | Details                                                      |
| ------------------ | ------------------------------------------------------------ |
| Serverspec         | Serverspec allows you to check if your servers are configured correctly and adhere to your policy requirements.<br>To test your servers, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra-inspec'})" style="text-decoration:none">provide your own ServerSpec code</a>. |
| Inspec             | InSpec allows you to check if your servers are configured correctly and adhere to your policy requirements.<br>To test your servers, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra-inspec'})" style="text-decoration:none">provide your own Inspec code</a>. |
| Azure Spec         | Azure Spec allows you to check if Azure resources have been deployed with the appropriate attribute values.<br>To test your Azure infrastructure, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'azure-infra'})" style="text-decoration:none">run an infrastructure test with custom Azure Spec code</a>. |
| AWS Spec           | AWS Spec allows you to check if AWS resources have been deployed with the appropriate attribute values. For example, you can check that the appropriate AMI has been used to deploy an EC2 instance.<br>To test your AWS infrastructure, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra-ui'})" style="text-decoration:none">run an infrastructure test with custom AWS Spec code</a>. |
| GCP Spec           | GCP Spec allows you to check if GCP resources have been deployed with the appropriate attribute values. To test your GCP infrastructure, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'gcp-infra'})" style="text-decoration:none">run an infrastructure test with custom GCP Spec code</a>. |

### <a id="infra-inspec" name="infra-inspec"></a>Run an infrastructure test with ServerSpec or InSpec code

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Infra**.

   The Infra Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_infratest.PNG)

   The procedure to configure an infrastructure test consists of three steps -- select the spec details, provide the codebase, and define execution details.

3. In the **BASICS** step, perform the following actions:

   - In **Job Name**, enter a unique name for your test job.
   - For **Spec Type**, select the appropriate specification type -- **Server Spec** or **InSpec**.
   - Enter the IP address, user name, and password or key of the server that you want to test.
   - Click **NEXT**.

4. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:
     
      - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 
      
        In the Upload File window, select the ZIP file and click **Upload Zip File**.
      
      - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:
      
        - GitHub repository clone URL
        - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
        - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*
      
   - Click **NEXT**.

5. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the infrastructure test code.

   - In **Test Run Command**, enter the command for running the infrastructure test code.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the infrastructure test code.

   - In **Output Directory**, enter the directory in which Test Accelerator must save the test run results. This path must be relative to the directory in which your infrastructure test code is stored.

   - In **Report File**, enter the name of the report file that Test Accelerator must generate after running the infrastructure test code.

6. In the right panel, verify that the details you have specified are correct.

7. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

8. Click **SUBMIT**.

9. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra-results'})" style="text-decoration:none">View the infrastructure test results</a>.

### <a id="azure-infra" name="azure-infra"></a>Run an infrastructure test with custom Azure Spec code

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Infra**.

   The Infra Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_azureinfratest.PNG)

   The procedure to configure an infrastructure test consists of three steps -- select the spec details, provide the codebase, and define execution details.

3. In the **BASICS** step, perform the following actions:

   - In **Job Name**, enter a unique name for your test job.

   - For **Spec Type**, select the **Azure Spec** specification type.

   - <a id="azure-prov" name="azure-prov"></a>Enter the following provider details to access your Azure account.

     | Attribute       | Details                                                      |
     | --------------- | ------------------------------------------------------------ |
     | subscription_id | A single Azure account can have multiple subscriptions. Enter the unique ID of your subscription to use Azure services. |
     | client_id       | Enter the ID of your application in Azure Active Directory.  |
     | client_secret   | Enter the authentication key for the specified application.  |
     | tenant_id       | Enter the ID of the Azure Active Directory tenant with which the specified subscription is associated. |

   - Click **NEXT**.

4. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*
   - Click **NEXT**.

5. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the Azure Spec code.

   - In **Test Run Command**, enter the command for running the Azure Spec code.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the Azure Spec code.

   - In **Output Directory**, enter the directory in which Test Accelerator must save the test run results. This path must be relative to the directory in which your Azure Spec code is stored.

   - In **Report File**, enter the name of the report file that Test Accelerator must generate after running the Azure Spec code.

   - If you want to upload a file that Test Accelerator must extract and provide while running your Azure Spec code, click **Upload File**. 

     In the Upload Input Output File window, select the appropriate file as a **ZIP** file and click **Upload File**.

     _**Note:**  Test Accelerator extracts the contents of this ZIP file in the **/home/seluser/hcaptest/code** folder of the instance that it launches to run the infrastructure test._

   - In the right panel, verify that the details you have specified are correct.

6. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

7. Click **SUBMIT**.

   When you start an **Azure Spec** infrastructure test job, Test Accelerator launches a test Kubernetes pod and downloads the infrastructure test code on the pod. It then connects to the Azure account for validating the infrastructure, and runs the test.

8. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

### <a id="infra-ui" name="infra-ui"></a>Run an infrastructure test with custom AWS Spec code

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Infra**.

   The Infra Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_awsinfratest.PNG)

   The procedure to configure an infrastructure test consists of three steps -- select the spec details, provide the codebase, and define execution details.

3. In the **BASICS** step, perform the following actions:

   - In **Job Name**, enter a unique name for your test job.

   - For **Spec Type**, select the **Aws Spec** specification type.

   - For **Credentials type**, perform the following actions:

     - Select **Basic Credentials**.
     - _(Optional)_ To use a more secure way of cross-account access, select **Assume Role**.

   - <a id="infra-provider-details" name="infra-provider-details"></a>Based on the selected credential type, specify the authentication details to access the AWS account in which you want to validate the infrastructure.

     - <a id="basic-assume" name="basic-assume"></a>**Basic Credentials with Assume Role**

       You can use this credential type when the AWS account for validating infrastructure is different from the AWS account in which Test Accelerator launches test instances.

       <u>Required actions and permissions</u>:

       To use this credential type, perform the following actions: 

       - In the AWS account for validating infrastructure, create a role that has **readonly** access to resources that need to be validated. This role must define as a trusted entity the AWS account for launching test instances.
       - In the AWS account in which the Test Accelerator is deployed, create an IAM user and attach a policy with STS permission to assume the role that you have created in the AWS account for validating infrastructure. 
     
       <u>Provider details</u>: 
       In the **Provider Details** section, specify the following details:
     
       - In **"access_key"** and **"secret_key"**, enter the access key and secret key of the IAM user that you have created in the AWS account. 
       - In **“assume_role”**, enter ARN of the role that you have created in the AWS account for validating infrastructure. You must also specify the session name and external ID. The specified IAM user assumes this role to validate the infrastructure. 
       - In **“region”**, enter the region in which the infrastructure must be validated.
     
       <u>JSON format with sample values</u>:

       ```
       {
        "access_key": "ACCESS-KEY",
        "secret_key": "SECRET-KEY",
        "region": "us-east-1",
        "assume_role": {
        "role_arn": " arn:aws:iam::XXXXXXXXXXXX:role/readonly-role",
        "session_name": "",
        "external_id": ""
        }
       ```

     - <a id="basic-creds" name="basic-creds"></a>**Basic Credentials**

       You can use this credential type in both scenarios: when the AWS account for validating infrastructure and the AWS account for launching instances is the same, or when they are two different accounts.

       <u>Required actions and permissions</u>:

       To use this credential type, create an IAM user in the AWS account for validating infrastructure and attach a policy with **readonly** access to resources that need to be validated.

       <u>Provider details</u>:

       In the **Provider Details** section, specify the following details:

       - In **"access_key"** and **"secret_key"**, enter the access key and secret key of the IAM user that you have created in the AWS account for validating infrastructure.
       - In **“region”**, enter the region in which the infrastructure must be validated.

       <u>JSON format with sample values</u>:

       ```
       {
         "access_key": "XXXX",
         "secret_key": "XXX",
         "region": "XXXX",
       }
       ```

     - <a id="basic-tempcreds" name="basic-tempcreds"></a>**Basic Credentials (using temporary credentials)**

       You can generate and use temporary credentials to access the AWS account for validating infrastructure. The temporary credentials that you specify can be for an IAM user or Assume Role.  

       <u>Required actions and permissions</u>:

       To use temporary credentials for an IAM user, perform the following actions:

       - In the AWS account for validating infrastructure, create an IAM user and attach a policy with **readonly** access to resources that need to be validated.
       - Generate temporary credentials for the IAM user.

       To use temporary credentials for an Assume Role, perform the following actions:

       - In the AWS account for validating infrastructure, create a role that has **readonly** access to resources that need to be validated. This role must define as a trusted entity the AWS account for launching test instances.
       - Generate temporary credentials for the role that you have created in the AWS account for validating infrastructure.

       <u>Provider details</u>:

       In the **Provider Details** section, specify the following details:

       - In **"access_key"** and **"secret_key"**, enter the temporary credentials that you have generated for the IAM user or Assume Role in the AWS account for validating infrastructure.
       - In **“region”**, enter the region in which the infrastructure must be validated.
       - In **"aws_session_token"**, enter the session token for the temporary credentials that you have generated.  

       <u>JSON format with sample values</u>

       ```
       {
         	"access_key": "ACCESS-KEY",
           "secret_key": "SECREt-KEY",
         	"region": "us-east-1",
           "aws_session_token": "SESSION-TOKEN"
       }    
       ```

       Click **NEXT**.

4. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*
     
   - Click **NEXT**.
   
5. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the AWS Spec code.

   - In **Test Run Command**, enter the command for running the AWS Spec code.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the AWS Spec code.

   - In **Output Directory**, enter the directory in which Test Accelerator must save the test run results. This path must be relative to the directory in which your AWS Spec code is stored.

   - In **Report File**, enter the name of the report file that Test Accelerator must generate after running the AWS Spec code.

   - If you want to upload a file that Test Accelerator must extract and provide while running your AWS Spec code, click **Upload File**. 

     In the Upload Input Output File window, select the appropriate file as a **ZIP** file and click **Upload File**.

     _**Note:** Test Accelerator extracts the contents of this ZIP file in the **/home/seluser/hcaptest/code** folder of the instance that it launches to run the infrastructure test._

6. In the right panel, verify that the details you have specified are correct.

7. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

8. Click **SUBMIT**.

   When you start an **AWS Spec** infrastructure test job, Test Accelerator launches a test Kubernetes pod and downloads the infrastructure test code on the pod. It then connects to the AWS account for validating the infrastructure, and runs the test.

9. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

### <a id="gcp-infra" name="gcp-infra"></a>Run an infrastructure test with custom GCP Spec code

1. On the Home page, click **New Test**.

2. In the Select Test window, click **Infra**.

   The Infra Test page appears, as shown in the following image.

   ![](/images/rean-test/rt_gcp.PNG)

   The procedure to configure an infrastructure test consists of three steps -- select the spec details, provide the codebase, and define execution details.

3. In the **BASICS** step, perform the following actions:

   - In **Job Name**, enter a unique name for your test job.

   - For **Spec Type**, select the **GCP Spec** specification type.

   - <a id="gcp-prov" name="gcp-prov"></a>Enter the following provider details to access your GCP account.

     | Attribute   | Details                                                      |
     | ----------- | ------------------------------------------------------------ |
     | project     | The project for managing GCP resources.                      |
     | credentials | The credentials can either be the path to, or the content of the GCP [service account key file](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) in JSON format. |

   - Click **NEXT**.

4. In the **CODEBASE** step, perform the following actions:

   - For **Automation Code**, select one of the following options:

     - If you want to upload your automation code as a ZIP file, select **Upload Code** and **Click to upload**. 

       In the Upload File window, select the ZIP file and click **Upload Zip File**.

     - If your automation code is available in a GitHub repository, select **Git**, and enter the following details about the GitHub repository:

       - GitHub repository clone URL
       - If your automation code is stored in a private repository, then select **Private Repository**, and enter your GitHub user ID and password. 
       - Branch name *(If you do not enter the branch name, Test Accelerator downloads the automation code from the **master** branch by default.)*

   - Click **NEXT**.

5. In the **EXECUTION** step, perform the following actions:

   - In **Pre-script**, enter any Shell script that Test Accelerator must run before running the GCP Spec code.

   - In **Test Run Command**, enter the command for running the GCP Spec code.

   - In **Post-script**, enter any Shell script that Test Accelerator must run after running the GCP Spec code.

   - In **Output Directory**, enter the directory in which Test Accelerator must save the test run results. This path must be relative to the directory in which your GCP Spec code is stored.

   - In **Report File**, enter the name of the report file that Test Accelerator must generate after running the GCP Spec code.

   - If you want to upload a file that Test Accelerator must extract and provide while running your GCP Spec code, click **Upload File**. 

     In the Upload Input Output File window, select the appropriate file as a **ZIP** file and click **Upload File**.

     _**Note:**  Test Accelerator extracts the contents of this ZIP file in the **/home/seluser/hcaptest/code** folder of the instance that it launches to run the infrastructure test._

   - In the right panel, verify that the details you have specified are correct.

6. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

7. Click **SUBMIT**.

   When you start an **GCP Spec** infrastructure test job, Test Accelerator launches a test Kubernetes pod and downloads the infrastructure test code on the pod. It then connects to the GCP account for validating the infrastructure, and runs the test.

8. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

## <a id="codeless" name="codeless"></a>Running codeless infra tests

The codeless infra test covers the testing of your AWS, Azure or GCP resources by using the default spec code that is provided by Test Accelerator. It saves time and resources spent on writing your own custom code.

1. Create an infrastructure test data JSON file. 

   For more information, see input and expected output JSON parameters for <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'IO-azure'})" style="text-decoration:none">Azure Spec</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'IO-aws'})" style="text-decoration:none">AWS Spec</a>, and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'IO-gcp'})" style="text-decoration:none">GCP Spec</a>

2. On the Home page, click **New Test**.

3. In the Select Test window, click **Codeless Infra**.

   The **Codeless Infra** test page appears, as shown in the following image.

   ![rt_securitytest.PNG](/images/rean-test/codeless1.png)

4. In the **Spec Type**, select **AWS Spec**, **Azure Spec**, **GCP Spec**.

5. In  **Name**, enter a unique name for your test job.

6. In the **Provider Details** section, specify the details provider details:

   - For AWS Spec, enter <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'basic-creds'})" style="text-decoration:none">basic credentials</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'basic-tempcreds'})" style="text-decoration:none">basic Credentials (using temporary credentials)</a>, or <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'basic-assume'})" style="text-decoration:none">basic credentials with assume role</a>.
   - For Azure Spec, enter the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'azure-prov'})" style="text-decoration:none">Azure provider details</a>.
   - For GCP Spec, enter the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'gcp-prov'})" style="text-decoration:none">GCP provider details</a>.
7. In the **Infrastructure Details** section, perform one of the following actions:

   - Select **JSON**, and enter the **Input** and **Expected Output JSON** parameters.
   - Select **Upload Input File**, and upload a zip file of the Input and Expected Output JSON parameters.

8. _(Optional)_ To run this test job multiple times based on a configured schedule, click **SCHEDULE**.

   For information about scheduling tests, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'scheduled-job'})" style="text-decoration:none">Scheduling test jobs</a>.

9. Click **SUBMIT**.

10. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'results'})" style="text-decoration:none">View and download test results</a>.

### <a id="IO-azure" name="IO-azure"></a>Create the infrastructure test data file for Azure Spec

To run an infrastructure test with Default Azure Spec code, you must first create a JSON file that contains the test data. Before you create a JSON file, see the list of <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'azure-resources'})" style="text-decoration:none">supported Azure resources</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'azure-versions'})" style="text-decoration:none">Azure spec versions</a>, 

#### Infrastructure JSON file

The following details are required to create the JSON file:

**Input:** This section contains the expected values that must be compared with the actual values that are retrieved for the resources defined in the **Output** section.

<u>Example JSON</u>

```json
"input": 
{
  "azurerm_snapshot": 
  {
    "testAzureSnapshot": 
	{
      "name": "sample_snapshot",
      "location": "East US",
      "resource_group_name": "sample_resources",
      "create_option": "Empty",
      "disk_size_gb": 10,
      "source_resource_id": null,
      "tags": {}
    }
  }
},
```

**Expected Output:** This section contains the names or IDs of all Azure resources that need to be validated.

<u>Example JSON</u>

```json
"output": 
{
	"azurerm_snapshot": 
	{
    "testAzureSnapshot": "sample_snapshot"
	}
}
```

#### <a id="azure-versions" name="azure-versions"></a>Supported versions for Azure Spec

The following table lists the Azure Spec code version that is available out of the box based on the version of Test Accelerator.

| Version of Test Accelerator                                  | Version of Default Azure Spec code |
| ------------------------------------------------------------ | ---------------------------------- |
| 2.22.3 and later                                             | 1.3                                |
| -- 2.22.2<br>-- 2.22.1<br>-- 2.21.0<br>-- 2.20.0<br>-- 2.19.0 | 1.1                                |
| <a id="azure-spec18" name="azure-spec18"></a>-- 2.18.0<br><a id="azure-spec18" name="azure-spec18"></a>-- 2.17.0 | 1.0                                |

#### <a id="azure-resources" name="azure-resources"></a>Supported resources for Azure Spec

The following table lists the resources that the Default Azure Spec code supports. The naming convention used for the supported resources is based on the HashiCorp Terraform resource names. 

| Resource Name                                     | Available Release Version |
| ------------------------------------------------- | ------------------------- |
| azurerm_resource_group                            | 1.0 and later             |
| azurerm_virtual_machine                           | 1.0 and later             |
| azurerm_virtual_network                           | 1.0 and later             |
| azurerm_virtual_machine_extension                 | 1.0 and later             |
| azurerm_network_interface                         | 1.0 and later             |
| azurerm_availability_set                          | 1.0 and later             |
| azurerm_public_ip                                 | 1.0 and later             |
| azurerm_subnet                                    | 1.0 and later             |
| azurerm_subnet_network_security_group_association | 1.0 and later             |
| azurerm_subnet_route_table_association            | 1.0 and later             |
| azurerm_image                                     | 1.0 and later             |
| azurerm_shared_image                              | 1.0 and later             |
| azurerm_shared_image_gallery                      | 1.0 and later             |
| azurerm_shared_image_version                      | 1.0 and later             |
| azurerm_lb                                        | 1.0 and later             |
| azurerm_snapshot                                  | 1.0 and later             |
| azurerm_local_network_gateway                     | 1.0 and later             |
| azurerm_lb_rule                                   | 1.0 and later             |
| azurerm_lb_backend_address_pool                   | 1.0 and later             |
| azurerm_lb_outbound_rule                          | 1.0 and later             |
| azurerm_lb_probe                                  | 1.0 and later             |
| azurerm_lb_nat_rule                               | 1.0 and later             |
| azurerm_lb_nat_pool                               | 1.0 and later             |
| azurerm_key_vault                                 | 1.0 and later             |
| azurerm_mysql_database                            | 1.0 and later             |
| azurerm_mysql_server                              | 1.0 and later             |
| azurerm_network_security_group                    | 1.0 and later             |
| azurerm_network_security_rule                     | 1.0 and later             |
| azurerm_network_profile                           | 1.0 and later             |
| azurerm_mysql_firewall_rule                       | 1.0 and later             |
| azurerm_mysql_configuration                       | 1.0 and later             |
| azurerm_virtual_network_peering                   | 1.0 and later             |
| azurerm_mysql_virtual_network_rule                | 1.0 and later             |
| azurerm_virtual_network_gateway                   | 1.0 and later             |
| azurerm_virtual_network_gateway_connection        | 1.0 and later             |
| azurerm_user_assigned_identity                    | 1.0 and later             |
| azurerm_api_management                            | 1.0 and later             |
| azurerm_api_management_user                       | 1.0 and later             |
| azurerm_api_management_group                      | 1.0 and later             |
| azurerm_api_management_product                    | 1.0 and later             |
| azurerm_api_management_group_user                 | 1.0 and later             |
| azurerm_api_management_api_operation              | 1.0 and later             |
| azurerm_api_management_property                   | 1.0 and later             |
| azurerm_api_management_api_operation_policy       | 1.0 and later             |
| azurerm_api_management_version_set                | 1.0 and later             |
| azurerm_api_management_api                        | 1.0 and later             |
| azurerm_route_table                               | 1.0 and later             |
| azurerm_route                                     | 1.0 and later             |
| azurerm_managed_disk                              | 1.0 and later             |
| azurerm_cdn_endpoint                              | 1.0 and later             |
| azurerm_cdn_profile                               | 1.0 and later             |
| azurerm_container_group                           | 1.0 and later             |
| azurerm_kubernetes_cluster                        | 1.0 and later             |
| azurerm_role_definition                           | 1.0 and later             |
| azurerm_role_assignment                           | 1.0 and later             |
| azurerm_postgresql_configuration                  | 1.0 and later             |
| azurerm_postgresql_database                       | 1.0 and later             |
| azurerm_postgresql_firewall_rules                 | 1.0 and later             |
| azurerm_batch_account                             | 1.0 and later             |
| azurerm_batch_pool                                | 1.0 and later             |
| azurerm_batch_certificate                         | 1.0 and later             |
| azurerm_storage_account                           | 1.0 and later             |
| azurerm_postgresql_server                         | 1.0 and later             |
| azurerm_postgresql_virtual_network_rule           | 1.0 and later             |
| azurerm_sql_database                              | 1.0 and later             |
| azurerm_sql_firewall_rule                         | 1.0 and later             |
| azurerm_sql_server                                | 1.0 and later             |
| azurerm_sql_virtual_network_rule                  | 1.0 and later             |
| azurerm_key_vault_access_policy                   | 1.0 and later             |
| azurerm_api_management_api_policy                 | 1.0 and later             |
| azurerm_api_management_api_schema                 | 1.0 and later             |
| azurerm_virtual_machine_data_disk_attachment      | 1.0 and later             |
| azurerm_redis_cache                               | 1.1 and later             |
| azurerm_app_service_plan                          | 1.1 and later             |
| azurerm_app_service                               | 1.1 and later             |
| azurerm_application_insights                      | 1.1 and later             |
| azurerm_cosmosdb_account                          | 1.1 and later             |
| azurerm_container_group                           | 1.1 and later             |
| azurerm_storage_container                         | 1.3 and later             |
| azurerm_cosmosdb_sql_database                     | 1.3 and later             |
| azurerm_key_vault_secret                          | 1.3 and later             |
| azurerm_cosmosdb_sql_container                    | 1.3 and later             |
| azurerm_logic_app_trigger_recurrence              | 1.3 and later             |
| azurerm_logic_app_trigger_custom                  | 1.3 and later             |
| azurerm_logic_app_trigger_http_request            | 1.3 and later             |
| azurerm_log_analytics_workspace                   | 1.3 and later             |
| azurerm_template_deployment                       | 1.3 and later             |
| azurerm_logic_app_workflow                        | 1.3 and later             |
| azurerm_logic_app_integration_account             | 1.3 and later             |
| azurerm_logic_app_action_http                     | 1.3 and later             |
| azurerm_logic_app_action_custom                   | 1.3 and later             |

### <a id="IO-aws" name="IO-aws"></a>Create the infrastructure test data file for AWS Spec

To run an infrastructure test with Default AWS Spec code, you must first create a JSON file that contains the test data.  Before you create a JSON file, see the list of <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'resources'})" style="text-decoration:none">supported AWS resources</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'aws-versions'})" style="text-decoration:none">AWS spec versions</a>.

#### Infrastructure JSON file

The following details are required to create the JSON file:

**Input**

This section contains the expected values that must be compared with the actual values that are retrieved for the resources defined in the **Output** section. 

A corresponding entry with the unique name specified in the **Output** section is configured in the **Input** section under the same resource type. Only the attributes defined in the **Input** section are compared with the actual state.

The resource type values in the **Input** section differ based on the version of the Default AWS Spec code. You can select one of the following options.

- Default AWS Spec code 1.3 and later

  In version 1.3, the resource type values are based on the Terraform resource names. For example, **aws_vpc** is the resource type under which VPC resources are defined. For details about the resource types that you must specify, see [Supported resources](https://reanplatform-help.reancloud.com/#/rean-platform-docs/accelerator?viewAccelerator=rean-test&viewPage=run-tests&viewSection=resources).

  Example JSON

  ```
  "input": {
    "aws_vpc": {
        "devVPC": {
            "cidr_block": "172.16.0.0/16",
            "tags": {
                "CreatedBy": "Deploy",
                "Name": "dev-datalake-quickstart-vpc",
                "Environment": "dev",
                "Owner": "a.g",
                "Product": "datalake-quickstart"
            },
            "enable_dns_support": true,
            "enable_dns_hostnames": true
        }
    }
  }
  ```

- Default AWS Spec code 1.2

  In version 1.2, the resource type values are based on custom types defined in Test Accelerator. For example, **VPC** is the resource type under which VPC resources are defined. For details about the resource types that you must specify, see [Resource types in Default AWS Spec code 1.2](https://reanplatform-help.reancloud.com/downloads/rean-test/Resource types in Default AWS Spec code 1.2.pdf).
  
  Example JSON

	```
	{
	    "VPC":{
		"vpc": {
		    "cidr_block": "10.0.0.0/16"
		}
	    },
	    "EC2": {
		"Demo_EC2_Instance": {
		    "instance_type": "t2.micro",
		    "tags": {
			"Name": "Platform-bastion-us-east-1b"
		    }
		}
	    }
	}
	```
	
	
	_**Note:** While Default AWS Spec code 1.3 is backward compatible and supports the older format of Input JSON, it is recommended that you switch to the latest format of Input JSON._

**Expected Output**

This section contains the names or IDs of all AWS resources that need to be validated.

Each key-value pair under each resource type represents the unique name of the resource and the corresponding ID of that resource. This ID is used to retrieve the attributes of the resource and validate them with the expected values defined in the **Input** section.

Example JSON

```
"output": {
    "aws_vpc": {
        "devVPC": "vpc-XXXXXXX",
        "prdVPC": "vpc-XXXXXXX"
    }
}
```

_**Note:** The resource type values in the **Output** section are based on the Terraform resource names. For example, in the above example, **aws_vpc** is used for the VPC resources._

#### <a id="aws-versions" name="aws-versions"></a>Supported versions for AWS Spec

The following table lists the Default AWS Spec code version that is available out of the box based on the version of Test Accelerator.

| Version of Test Accelerator                                  | Version of Default AWS Spec code |
| ------------------------------------------------------------ | -------------------------------- |
| 2.22.1 and later                                             | 1.5                              |
| -- 2.20.0<br>-- 2.19.0<br>-- 2.18.0<br>-- 2.17.0<br>-- 2.16.0<br>-- 2.15.0 | 1.4                              |
| 2.14.0                                                       | 1.3                              |
| 2.13.0                                                       | 1.3                              |
| 2.12.0                                                       | 1.2                              |

#### <a id="resources" name="resources"></a>Supported resources for AWS Spec

The following table lists the resources that the Default AWS Spec code supports. The naming convention that is used for the supported resources is based on the HashiCorp Terraform resource names. 

| Resource Name                         | Available Release Version |
| ------------------------------------- | ------------------------- |
| aws_instance                          | 1.2 and later             |
| aws_vpc                               | 1.2 and later             |
| aws_vpc_peering_connection            | 1.2 and later             |
| aws_subnet                            | 1.2 and later             |
| aws_route_table                       | 1.2 and later             |
| aws_security_group                    | 1.2 and later             |
| aws_network_acl                       | 1.2 and later             |
| aws_autoscaling_group                 | 1.2 and later             |
| aws_launch_configuration              | 1.2 and later             |
| aws_elb                               | 1.2 and later             |
| aws_nat_gateway                       | 1.2 and later             |
| aws_internet_gateway                  | 1.2 and later             |
| aws_eip                               | 1.2 and later             |
| aws_launch_template                   | 1.2 and later             |
| aws_efs_file_system                   | 1.2 and later             |
| aws_efs_mount_target                  | 1.2 and later             |
| aws_iam_group                         | 1.2 and later             |
| aws_iam_role                          | 1.2 and later             |
| aws_iam_policy                        | 1.2 and later             |
| aws_iam_instance_profile              | 1.2 and later             |
| aws_iam_user                          | 1.2 and later             |
| aws_flow_log                          | 1.2 and later             |
| aws_vpc_endpoint                      | 1.2 and later             |
| aws_cloudwatch_log_group              | 1.2 and later             |
| aws_route_table_association           | 1.2 and later             |
| aws_sns_topic                         | 1.2 and later             |
| aws_sns_topic_policy                  | 1.2 and later             |
| aws_sns_topic_subscription            | 1.2 and later             |
| aws_redshift_cluster                  | 1.2 and later             |
| aws_redshift_subnet_group             | 1.2 and later             |
| aws_elasticsearch_domain              | 1.2 and later             |
| aws_lb_target_group                   | 1.2 and later             |
| aws_alb                               | 1.2 and later             |
| aws_customer_gateway                  | 1.2 and later             |
| aws_db_option_group                   | 1.2 and later             |
| aws_db_parameter_group                | 1.2 and later             |
| aws_db_subnet_group                   | 1.2 and later             |
| aws_db_instance                       | 1.2 and later             |
| aws_rds_cluster                       | 1.2 and later             |
| aws_sqs_queue                         | 1.2 and later             |
| aws_sqs_queue_policy                  | 1.2 and later             |
| aws_vpn_gateway                       | 1.2 and later             |
| aws_vpn_connection                    | 1.2 and later             |
| aws_dynamodb_table                    | 1.2 and later             |
| aws_ses_active_receipt_rule_set       | 1.2 and later             |
| aws_ses_receipt_rule                  | 1.2 and later             |
| aws_ses_receipt_rule_set              | 1.2 and later             |
| aws_ses_receipt_filter                | 1.2 and later             |
| aws_ses_domain_identity               | 1.2 and later             |
| aws_ses_configuration_set             | 1.2 and later             |
| aws_ses_event_destination             | 1.2 and later             |
| aws_alb_listener                      | 1.2 and later             |
| aws_alb_listener_rule                 | 1.2 and later             |
| aws_elb_load_balancer_listener_policy | 1.2 and later             |
| aws_route53_health_check              | 1.2 and later             |
| aws_route53_zone                      | 1.2 and later             |
| aws_route53_record                    | 1.2 and later             |
| aws_kms_key                           | 1.4 and later             |
| aws_kms_alias                         | 1.4 and later             |
| aws_s3_bucket                         | 1.4 and later             |
| aws_iam_role_policy                   | 1.4 and later             |
| aws_iam_group_policy                  | 1.4 and later             |
| aws_kinesis_stream                    | 1.4 and later             |
| aws_cloudtrail                        | 1.4 and later             |
| aws_codecommit_repository             | 1.4 and later             |
| aws_security_group_rule               | 1.4 and later             |
| aws_volume_attachment                 | 1.4 and later             |
| aws_swf_domain                        | 1.4 and later             |
| aws_key_pair                          | 1.4 and later             |
| aws_ami                               | 1.4 and later             |
| aws_lambda_function                   | 1.4 and later             |
| aws_s3_bucket_object                  | 1.4 and later             |
| aws_s3_bucket_policy                  | 1.4 and later             |
| aws_ebs_volume                        | 1.4 and later             |
| aws_route                             | 1.4 and later             |
| aws_alb_target_group                  | 1.4 and later             |
| aws_vpc_peering_connection_accepter   | 1.4 and later             |
| aws_ecs_service                       | 1.4 and later             |
| aws_ecr_lifecycle_policy              | 1.4 and later             |
| aws_ecr_repository_policy             | 1.4 and later             |
| aws_alb_target_group                  | 1.4 and later             |
| aws_iam_policy_attachment             | 1.4 and later             |
| aws_vpc_dhcp_options_association      | 1.4 and later             |
| aws_iam_group_policy_attachment       | 1.4 and later             |
| aws_iam_role_policy_attachment        | 1.4 and later             |
| aws_ecs_cluster                       | 1.4 and later             |
| aws_appautoscaling_target             | 1.4 and later             |
| aws_alb_listener_certificate          | 1.4 and later             |
| aws_vpc_dhcp_options                  | 1.4 and later             |
| aws_alb_target_group_attachment       | 1.4 and later             |
| aws_spot_instance_request             | 1.4 and later             |
| aws_iam_server_certificate            | 1.4 and later             |
| aws_network_interface                 | 1.4 and later             |
| aws_ecr_repository                    | 1.4 and later             |
| aws_eip_association                   | 1.4 and later             |
| aws_elasticache_security_group        | 1.4 and later             |
| aws_elasticache_subnet_group          | 1.4 and later             |
| aws_lb_cookie_stickiness_policy       | 1.4 and later             |
| aws_s3_bucket_notification            | 1.4 and later             |
| aws_elasticache_replication_group     | 1.4 and later             |
| aws_autoscaling_policy                | 1.4 and later             |
| aws_autoscaling_notification          | 1.4 and later             |
| aws_autoscaling_attachment            | 1.4 and later             |
| aws_autoscaling_lifecycle_hook        | 1.4 and later             |
| aws_elasticache_parameter_group       | 1.4 and later             |
| aws_placement_group                   | 1.4 and later             |
| aws_api_gateway_api_key               | 1.4 and later             |
| aws_ebs_snapshot                      | 1.4 and later             |
| aws_autoscaling_schedule              | 1.4 and later             |

### <a id="IO-gcp" name="IO-gcp"></a>Create the infrastructure test data file for GCP Spec

To run an infrastructure test with Default GCP Spec code, you must first create a JSON file that contains the test data. Before you create a JSON file, see the list of <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'gcp-resources'})" style="text-decoration:none">supported GCP resources</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'gcp-versions'})" style="text-decoration:none">GCP Spec versions</a> supported by Test Accelerator.

#### Infrastructure JSON file

The following details are required to create the JSON file:

**Input:** This section contains the expected values that must be compared with the actual values that are retrieved for the resources defined in the **Output** section.

<u>Example JSON</u>

```json
 "input": {
    "google_compute_address": {
      "address": {
        "name": "ip-bastion-host",
        "description":"test gcpspec",
        "labels":{
          "owner":"hcap-test",
          "environment":"development"
        },
        "address":"10.0.0.26",
        "address_type":"INTERNAL",
        "purpose":"GCE_ENDPOINT",
        "network_tier":"PREMIUM",
        "subnetwork":"subnet-hv-hcap-dev-central",
        "region":"us-central1",
        "project":"hv-hcap-development"
      }
    }
  },
```

**Expected Output:** This section contains the names or IDs of all Azure resources that need to be validated.

<u>Example JSON</u>

```json
 "output": {
    "google_compute_address": {
      "address": "hcap-disk"
    }
  }
```

#### <a id="gcp-versions" name="gcp-versions"></a>Supported versions for GCP Spec

The following table lists the GCP Spec code version that is available out of the box based on the version of Test Accelerator.

| Version of Test Accelerator                    | Version of Default GCP Spec code |
| ---------------------------------------------- | -------------------------------- |
| <a id="gcp-spec18" name="gcp-spec18"></a>3.2.0 | 1.1                              |

#### <a id="gcp-resources" name="gcp-resources"></a>Supported resources for GCP Spec

The following table lists the resources that the Default GCP Spec code supports. The naming convention used for the supported resources is based on the HashiCorp Terraform resource names. 

| Resource Name                         | Available Release Version |
| ------------------------------------- | ------------------------- |
| google_compute_instance               | 1.1 and later             |
| google_compute_network                | 1.1 and later             |
| google_compute_subnetwork             | 1.1 and later             |
| google_compute_disk                   | 1.1 and later             |
| google_compute_machine_image          | 1.1 and later             |
| google_compute_firewall               | 1.1 and later             |
| google_compute_router                 | 1.1 and later             |
| google_compute_instance_template      | 1.1 and later             |
| google_compute_image                  | 1.1 and later             |
| google_compute_address                | 1.1 and later             |
| google_compute_router_nat             | 1.1 and later             |
| google_compute_autoscaler             | 1.1 and later             |
| google_compute_instance_group_manager | 1.1 and later             |
| google_storage_bucket_acl             | 1.1 and later             |
| google_storage_bucket                 | 1.1 and later             |
| google_storage_default_object_acl     | 1.1 and later             |
| google_compute_vpn_gateway            | 1.1 and later             |
| google_compute_target_instance        | 1.1 and later             |
| google_compute_route                  | 1.1 and later             |
| google_compute_instance_group         | 1.1 and later             |
| google_compute_target_pool            | 1.1 and later             |
| google_compute_node_group             | 1.1 and later             |
| google_compute_network_endpoint_group | 1.1 and later             |
| google_container_node_pool            | 1.1 and later             |
| google_compute_ssl_policy             | 1.1 and later             |
| google_compute_ssl_certificate        | 1.1 and later             |
| google_compute_snapshot               | 1.1 and later             |

## <a id="results" name="results"></a>Viewing and downloading test results

The Home page of Test Accelerator displays a summary of the total number of test cases that have passed and the total number of builds that are ready for release, as shown in the following image.

![](/images/rean-test/rt_testsummary.PNG)

**To view and download the test results of a specific job, perform the following actions:**

1. On the Home page of Test Accelerator, from the left panel, select the test job whose details you want to view. 

   In the menu bar, you can view details such as when the job was last run and the total number of browsers that are in the **Configuring**, **Running**, **Success**, and **Failed** status. 

   ![](/images/rean-test/rt_testbubbles.PNG)

   In the right panel, each bubble represents a browser in the selected test job. The size of the bubble represents the time taken by the test run and the color represents the state (Configuring, Running, Success, and Failed). If you hover over a bubble, you can view details about the browser it represents.

2. *(Optional)* To filter the list of test jobs, perform the following actions:

   - To filter the job list based on keywords or the job ID, use the search box.

   - To view only scheduled jobs, select the **Scheduled** check box.

   - To view only your own jobs, select the **Owned by me** check box.

     This check box is helpful when you are part of a shared group and can view the jobs created by other users in that group.

   - To view only your own scheduled jobs, select the **Owned by me** and **Scheduled** check boxes.

3. _(Optional)_ To view the actual tests that are running on a browser, click the bubble for that browser when it is in the **Running** state.

4. To view and download the report of a test run, perform the following actions:

   - To view the report of a test run for a specific browser, click the bubble for that browser when it is in the **Success** or **Failed** state.

      The HTML report displays the result of the automation suite for the selected browser. The test results include a screenshot for each test case that is run on the browser.

      ![](/images/rean-test/rt_testresults.PNG)

   - To download the report for a specific browser, right-click the bubble for that browser, and select **Download Reports**. 

     ![](/images/rean-test/logs1.PNG)
     
   - To download the report of a test run for all selected browsers, click the **Download Report** icon (![](/images/rean-test/icon_downloadreport.PNG)).

     A ZIP file is downloaded to your local computer. When you extract the contents of the ZIP file, you can see a folder for each browser version. To view the HTML report for a browser version, click the folder for that browser version and extract the contents of the **reports.zip** file.

5. To view and download a summary report of the test run for all browsers, perform the following actions:

   - Click the **Full Report** icon (![](/images/rean-test/icon_fullreport.PNG)) in the menu bar.

      The consolidated report enables you to analyze the test results at any time while a job is in the **Running** state.

      ![](/images/rean-test/rt_consolidatedrun.PNG)

   - To download the summary report, click **ExportToExcel** or **ExportToCSV**. 

6. _(Only for infrastructure test jobs)_ To view the infrastructure test report, perform the following actions:

   - From the left panel, select the infrastructure test job whose details you want to view. 

   - To view detailed reports for the selected infrastructure job, in the **Reports** panel, select the appropriate **Report** link.

     _**Note:** The Infra Dashboard displays a consolidated report for each resource type in the selected infrastructure job._

     ![](/images/rean-test/rt_infradashboard.PNG)

   - *(Optional)* To download a report for the selected infrastructure job, perform the following actions:

     - To download an Excel report that contains the test summary and detailed test analytics, click **ExportToExcel**.
     - To download a ZIP file that contains detailed HTML reports for each resource type, click **Download Report**.

_**Important:** To use the reporting feature in Test Accelerator, your automation suite must have a valid reporting framework that enables creation of reports in HTML and JSON formats. Test Accelerator does not create reports but instead, displays reports that are created by your automation suite. While creating a test job, you must specify the relative path to the home directory of the automation suite and enter the JSON format file._ 

## <a id="logs" name="logs"></a>Viewing and downloading logs 

From the Test accelerator home page, you can download logs for the ongoing and completed tests. To view and download logs for a test run, perform the following actions:

- To view the logs, right-click the bubble, and select **Get Logs**. 

  ![](/images/rean-test/logs1.PNG)
  
- To download the logs, right-click the bubble, and select **Download Logs**.

## <a id="jobs-list" name="jobs-list"></a>Viewing jobs list

1. On the Home page of Test Accelerator, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner.

2. Click **Job List**.

   On the Test Job List page, you can view the list of all test jobs that you have created and the test jobs that are shared with you. You can also view the job type, creation date, and status.

3. _(Optional)_ To filter the list of test jobs, enter appropriate keywords in the Search box. 

## <a id="stop" name="stop"></a>Stopping test jobs

1. On the Home page of Test Accelerator, from the left panel, select the test job that you want to stop.
2. In the menu bar, click the **Abort** icon (![](/images/rean-test/icon_stop.PNG)).
4. In the confirmation message box, click **YES**.

## <a id="rerun" name="rerun"></a>Rerunning test jobs

1. On the Home page of Test Accelerator, from the left panel, select the test job that you want to rerun.

2. In the menu bar, click the **Re-run** icon (![](/images/rean-test/icon_rerun.PNG)).

3. _(Optional)_ Update the job details based on your requirements.

   For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'url'})" style="text-decoration:none">Running URL tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'manual'})" style="text-decoration:none">Running manual tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'security'})" style="text-decoration:none">Running security tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'automated'})" style="text-decoration:none">Running automated tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'load'})" style="text-decoration:none">Running scale tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'infra'})" style="text-decoration:none">Running infrastructure tests</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'codeless'})" style="text-decoration:none">Running codeless infrastructure tests</a>, and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'api'})" style="text-decoration:none">Running API tests</a>.

   _**Note:** The password for Git repository is not stored in the test job. You must re-enter the Git password in the **CODEBASE** step of the test jobs._

5. Submit the test job.

   A new test job appears in the jobs list.


## <a id="scheduled-job" name="scheduled-job"></a>Scheduling test jobs

1. On the Home page of Test Accelerator, from the left panel, select the test job that you want to run multiple times based on a configured schedule.

2. In the menu bar, click the **Schedule** icon (![](/images/rean-test/icon_schedule.PNG)).

3. In the Schedule Job window, enter the schedule name.

   ![](/images/rean-test/rt_schedulejob.PNG)

5. To define how frequently the job must be run, for **Repeats** and **Repeat every**, select the appropriate options.

6. To define when the scheduled jobs must start and end, for **Starts** and **Ends**, select the appropriate options.

7. Click **SCHEDULE**.

   Test Accelerator creates and displays the first test job in the job list. Additional test jobs are added to this list based on the schedule that you have configured.

7. _(Optional)_ To view the scheduled test jobs, in the left panel on the Home page, select **Scheduled**.

   ![](/images/rean-test/rt_scheduledjob_toggle.PNG)

   The list displays the name that you provided while scheduling the test jobs. You can search for a specific schedule name to view all test jobs that have been created based on that schedule.

## <a id="schedule-list" name="schedule-list"></a>Managing job schedules

Each time you schedule a test job, Test Accelerator creates a corresponding job schedule. You can view the list of all job schedules that have been created and the status of each schedule (Scheduled, Running, Completed, Failed, and Aborted).

1. On the Home page of Test Accelerator, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner.

2. Click **Schedule**.

   The Schedule List page displays all the job schedules that have been created. The **Name** column displays the name that was provided while scheduling test jobs.

2. To view details about a job schedule, click that schedule in the Schedule list.

   The right panel displays a summary about the selected job schedule. You can also view the date and time when the next test job is scheduled to run.  

   ![](/images/rean-test/rt_jobschedule_list.PNG)

3. To abort a job schedule, click the **Actions** icon (![](/images/rean-test/icon_actions.PNG)) for that job schedule, and click **Abort**.

   The **Abort** option is available only for job schedules with the **Scheduled** status. When you abort a schedule, corresponding future scheduled jobs are no longer created. 

5. To pause a job schedule, click the **Actions** icon (![](/images/rean-test/icon_actions.PNG)) for that job schedule, and click **Pause**.

   The **Pause** option is available only for job schedules with the **Scheduled** status. When you pause a schedule, corresponding future scheduled jobs are not created until you resume the job schedule.

   To resume a paused job schedule, click the **Actions** icon (![](/images/rean-test/icon_actions.PNG)) for that job schedule, and click **Resume**. 

6. To delete a job schedule from the list, click the **Actions** icon (![](/images/rean-test/icon_actions.PNG)) for that job schedule, and click **Remove**.

   When you delete a job schedule, corresponding future scheduled jobs are no longer created.

