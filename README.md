# End Test fetch API

Steps:-
1. setup mongo
2. create database "EndTest"
3. Setup usename and pass as root,root respectively in "EndTest" database 
4. create 2 collection as "EndTestProjectSuiteLinking" and "endTest"
5. download json for endtest suite from endtest website and then upload it to "endTest" collection
6. run command:- mvn clean install -U 
7. run command:-  java -jar target/endtest-1.0-SNAPSHOT.jar
8. wait for given log "Started EndTestApplication" in terminal
9. open new terminal
10. open endTestPage and inspect element.
11. open browser console
12. type "appID" and hit enter. this will give you AppID
13. type "appCode" and hit enter. this will give you appCode
14. run below api:- 
15. curl --location --request GET 'http://localhost:9990/endTest/getSuiteTestIdDateAndSaveInLinkingDB?appId=<appID>&appCode=<APP_code>'
16. run command:- mvn test -P transform
17. above command will create .txt for all suite added in mongo
18. run command: mvn test -P DynamicSuite -DsuiteXml=TestSuiteXMLCreation.xml
19. above command will create xml runner files and selenium code for each suite.
20. set Lambdatest credential via below command. https://automation.lambdatest.com/timeline/?viewType=build&page=1
21. run command:- export LT_USERNAME="<lambdatest Automation username>"
22. run command:- export LT_ACCESS_KEY="<lambdatest Automation key>"
23. run each suite via command:-  mvn test -P testNGRunner -DsuiteXml=<suitename>.xml


Run cucumber features Files:-

1. create cucucmber.yaml in location src/main/java/cucumberRunnerFiles/testrunner/cucumber.yaml and add key and username for Lambdatest in cucumber.yaml. Do not rename existing sample file. it will push your credential in code.
2. create feature file for each java suite file in src/main/java/features
3. create a test as a scenario in each feature file.
4. create step def in src/main/java/StepDef
5. steps will be plan text don't take variables for default steps as your int value in name will be treated as variable.
6. use the below command to run your test. CUCUMBER_FILTER_TAGS=<Tag> mvn test -P cucumberRun  -DsuiteXmlFile=<parallel count xml> -DJENKINS_JOB_IDENTIFIER=<unique build name. use ${BUILD_ID} if using jenkins>
7. eg:- CUCUMBER_FILTER_TAGS=@regression_colombia_ecom_1 mvn test -P cucumberRun  -DsuiteXmlFile=5Parallel.xml -DJENKINS_JOB_IDENTIFIER=Run1
8. @mobile tag will run on mobile. if not given then it will run on desktop based on Hook.java file code.
9. Command to run on different browser/device 
10. CUCUMBER_FILTER_TAGS=@mobile mvn test -P cucumberRun  -DsuiteXmlFile=100Parallel.xml -DJENKINS_JOB_IDENTIFIER="noMobile9" -DGIVEN_CLIENT_CAPS="platformName=Android,deviceName=Galaxy S10 Lite,platformVersion=11"
11. CUCUMBER_FILTER_TAGS=@mobile mvn test -P cucumberRun  -DsuiteXmlFil
    e=100Parallel.xml -DJENKINS_JOB_IDENTIFIER="noMobile9" -DGIVEN_CLIENT_CAPS="platformName=Android,deviceName=Galaxy S10 Lite,platformVersion=11"



