newman
Guidelines on installation NODE JS and NPM
https://docs.npmjs.com/downloading-and-installing-node-js-and-npm

How to install Newman:
https://www.npmjs.com/package/newman#getting-started

Working with Newman (complete guide)
https://www.npmjs.com/package/newman

For macOS users
If you fail to run command $ npm install -g newman
Try running it with sudo (super user do command)
sudo npm install -g newman
It will prompt you for admin password and run the command to install Newman

cd Desktop\ASK-Tests
dir

newman run ASK_Tests.postman_collection.json -e ASK_QA.postman_environment.json

newman run ASK_Tests.postman_collection.json -e ASK_QA.postman_environment.json

Результаты теста на экран
newman run DataVariables.postman_collection.json -e ASK_QA.postman_environment.json -d Data.csv

Результаты теста в файл
newman run DataVariables.postman_collection.json -e ASK_QA.postman_environment.json -d Data.csv > results.txt

Генерация базы данных для тестирования
npm install -g xmysql

xmysql -h 44.205.92.189 --port 3308 -u testuser -p password -d application 
чтобы связать Постман с базой данных (реквизиты базы)


ASK_Tests

→ /sign-up - [S] New user and sends verification email
  POST http://ask-qa.portnov.com/api/v1/sign-up [200 OK, 569B, 1230ms]
  √  Status code is 200
  √  Response message = User was created

→ localhost:3000/ - New Student activationCode
  GET localhost:3000/api/users?_where=(email,eq,abc2024@test.com) [200 OK, 576B, 179ms]
  √  Status code is 200

→ /activate/idS/actCode
  GET http://ask-qa.portnov.com/api/v1/activate/12951/2a14e16b7d7bee7f3c6384e15f83b88bed22170c [200 OK, 571B, 109ms]
  √  Status code is 200
  √  Message - User was activated

→ /sign-in - [T]
  POST http://ask-qa.portnov.com/api/v1/sign-in [200 OK, 873B, 93ms]
  √  Status code is 200
  √  Response time is less than 2000ms
  √  Verify user role = TEACHER

→ /sign-in - [T] - Invalid Password
  POST http://ask-qa.portnov.com/api/v1/sign-in [404 Not Found, 409B, 96ms]
  √  Status code is 404 - Authentication failed. User not found or password does not match

→ /sign-in - [S]
  POST http://ask-qa.portnov.com/api/v1/sign-in [200 OK, 872B, 102ms]
  √  Status code is 200
  √  Response time is less than 2000ms
  √  Verify user role = STUDENT

→ /quiz -[T] Create a new quiz
  POST http://ask-qa.portnov.com/api/v1/quiz [200 OK, 792B, 101ms]
  √  Status code is 200
  √  Response time is less than 2000ms

→ /quizzes - [T] List of quizzes
  GET http://ask-qa.portnov.com/api/v1/quizzes [200 OK, 290.2kB, 467ms]
  √  Status code is 200
  √  Response time is less than 2000ms
  √  Verify the number of quiz created

→ /assignment - [T] New assignment
  POST http://ask-qa.portnov.com/api/v1/assignment [200 OK, 1.65kB, 117ms]
  √  Status code is 200
  √  Response time is less than 2000ms
  √  Verify the status, result, and gradedBy of assignment befor submission

→ /submit-assignment - [S]
  POST http://ask-qa.portnov.com/api/v1/submit-assignment [200 OK, 1.82kB, 105ms]
  √  Status code is 200
  √  Status, result, gradedBy - after submission

→ /assignment/:assignmentId - [T] Manual grading
  PUT http://ask-qa.portnov.com/api/v1/assignment/26646 [200 OK, 1.64MB, 1590ms]
  √  Status code is 200
  √  Status, result, and gradedBy after manual grading

→ /quiz/id - [T]
  DELETE http://ask-qa.portnov.com/api/v1/quiz/24216 [200 OK, 751B, 103ms]
  √  Status code is 200
  √  Message - Quiz was deleted

→ /assignment/:assignmentGroupID - [T]
  DELETE http://ask-qa.portnov.com/api/v1/assignment/a6def280-ed4f-4379-99d1-633a03b6cbd6 [200 OK, 757B, 99ms]
  √  Status code is 200
  √  Body matches string - Assignment was deleted

→ /forgot-password - [S]
  POST http://ask-qa.portnov.com/api/v1/forgot-password [200 OK, 582B, 748ms]
  √  Status code is 200
  √  Body matches string - Reset password email was sent

→ localhost:3000/ - Reset passwordS activationCode
  GET localhost:3000/api/users?_where=(email,eq,abc2024@test.com) [200 OK, 576B, 176ms]
  √  Status code is 200

→ /reset-password/:userId/:activationCode - [S]
  POST http://ask-qa.portnov.com/api/v1/reset-password/12951/215a6d88d20a6e02c52538e5c11e40fed88b4144 [200 OK, 573B, 96ms]
  √  Status code is 200
  √  Body matches string - Password was changed

→ /users/change-role/studentId - [T]
  PUT http://ask-qa.portnov.com/api/v1/users/change-role/12951 [200 OK, 756B, 94ms]
  √  Status code is 200
  √  Body matches string - User role was updated

→ /users/:userId - [T]
  DELETE http://ask-qa.portnov.com/api/v1/users/12951 [200 OK, 756B, 100ms]
  √  Status code is 200
  1. Body matches string - User was deleted

┌─────────────────────────┬─────────────────────┬────────────────────┐
│                         │            executed │             failed │
├─────────────────────────┼─────────────────────┼────────────────────┤
│              iterations │                   1 │                  0 │
├─────────────────────────┼─────────────────────┼────────────────────┤
│                requests │                  18 │                  0 │
├─────────────────────────┼─────────────────────┼────────────────────┤
│            test-scripts │                  18 │                  0 │
├─────────────────────────┼─────────────────────┼────────────────────┤
│      prerequest-scripts │                   0 │                  0 │
├─────────────────────────┼─────────────────────┼────────────────────┤
│              assertions │                  37 │                  1 │
├─────────────────────────┴─────────────────────┴────────────────────┤
│ total run duration: 7.4s                                           │
├────────────────────────────────────────────────────────────────────┤
│ total data received: 1.93MB (approx)                               │
├────────────────────────────────────────────────────────────────────┤
│ average response time: 311ms [min: 93ms, max: 1590ms, s.d.: 425ms] │
└────────────────────────────────────────────────────────────────────┘

[31m  # [39m[31m failure        [39m[31m detail                                                                          [39m
[90m    [39m[90m                [39m[90m                                                                                 [39m
 1.  AssertionError  Body matches string - User was deleted                                          
                     expected '{"status":"success","message":"User r…' to include 'User was deleted' 
                     at assertion:1 in test-script                                                   
                     inside "/users/:userId - [T]"                                                   
