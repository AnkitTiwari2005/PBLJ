# SmartQuizApp 🎯

A modern, feature-rich online quiz application built with Spring Boot that allows admins to create quizzes and students to take them with real-time scoring and leaderboards.

## ✨ Features

### 🎓 For Students
- **Take Quizzes**: Participate in available quizzes with timed sessions
- **Real-time Timer**: Countdown timer for each quiz attempt  
- **Instant Results**: Immediate scoring after quiz submission
- **Leaderboards**: View rankings and compare performance with peers
- **User Registration**: Simple sign-up process

### 👨‍💼 For Admins
- **Quiz Management**: Create, edit, and delete quizzes
- **Question Bank**: Add multiple-choice questions with options
- **Automatic Scoring**: System automatically evaluates and scores attempts
- **Analytics**: View quiz statistics and performance metrics
- **User Management**: Monitor student progress and results

## 🚀 Quick Start

### Prerequisites
- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+

### Installation & Running

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd SmartQuizApp
Database Setup

sql
CREATE DATABASE smartquizapp;
Configure Database
Update src/main/resources/application.properties with your MySQL credentials:

properties
spring.datasource.username=your_username
spring.datasource.password=your_password
Build and Run

bash
mvn clean package spring-boot:run
Access the Application

Open: http://localhost:8080

Default admin: admin / admin

Register new students or use demo accounts

🏗️ Project Structure
text
src/main/java/com/example/smartquizapp/
├── controller/          # MVC Controllers
│   ├── AdminController.java
│   ├── AuthController.java
│   └── QuizController.java
├── model/              # JPA Entities
│   ├── User.java
│   ├── Quiz.java
│   ├── Question.java
│   └── Attempt.java
├── repository/         # Data Access Layer
│   ├── UserRepository.java
│   ├── QuizRepository.java
│   ├── QuestionRepository.java
│   └── AttemptRepository.java
├── service/           # Business Logic
│   └── QuizService.java
└── SmartQuizAppApplication.java
🎯 Core Features Explained
Quiz System
Timed Quizzes: Configurable duration for each quiz

Multiple Choice: Support for 2-4 options per question

Automatic Evaluation: Real-time scoring with detailed feedback

Score Tracking: Persistent attempt history with timestamps

User Management
Role-based Access: Separate interfaces for admins and students

Session Management: Secure login with proper session handling

Progress Tracking: Individual attempt history and statistics

Leaderboard & Analytics
Real-time Rankings: Live leaderboard updates

Performance Metrics: Average scores, completion rates, and high scores

Comparative Analysis: See how you stack up against peers

🛠️ Technology Stack
Backend: Spring Boot 3.2.5, Spring MVC, Spring Data JPA

Frontend: Thymeleaf, Bootstrap 5, JavaScript

Database: MySQL 8.0 with Hibernate ORM

Build Tool: Maven

Java Version: 17

📊 Database Schema
sql
user        -> id, username, password, role(ADMIN/STUDENT), created_at
quiz        -> id, title, duration_seconds, created_by, created_at  
question    -> id, quiz_id, text, option_a/b/c/d, correct_option, marks
attempt     -> id, student_id, quiz_id, score, max_score, started_at, finished_at
🎨 UI/UX Features
Responsive Design: Works on desktop, tablet, and mobile

Modern Interface: Clean, professional look with gradient backgrounds

Interactive Elements: Animated cards, hover effects, and smooth transitions

User-friendly Forms: Validation and helpful error messages

Professional Typography: Inter font family for better readability

🔧 API Endpoints
Authentication
GET/POST /login - User login

GET/POST /register - User registration

GET /logout - User logout

Student Features
GET /quizzes - List all available quizzes

GET /quizzes/{id}/start - Start a quiz

POST /quizzes/{id}/submit - Submit quiz answers

GET /quizzes/{id}/leaderboard - View quiz leaderboard

Admin Features
GET /admin/dashboard - Admin control panel

GET/POST /admin/quiz/new - Create new quiz

GET/POST /admin/quiz/{id}/question/new - Add questions to quiz

POST /admin/quiz/{id}/delete - Delete quiz

⚙️ Configuration
Application Properties
properties
# Server
server.port=8080
server.servlet.session.timeout=1800

# Database
spring.datasource.url=jdbc:mysql://localhost:3306/smartquizapp
spring.jpa.hibernate.ddl-auto=update

# Thymeleaf
spring.thymeleaf.cache=false
spring.thymeleaf.prefix=classpath:/templates/

# Logging
logging.level.com.example.smartquizapp=DEBUG
Custom Settings
Default quiz duration: 300 seconds (5 minutes)

Default question marks: 5 points

Maximum questions per quiz: 50

🐛 Troubleshooting
Common Issues
Database Connection Failed

Verify MySQL is running

Check credentials in application.properties

Ensure database smartquizapp exists

Build Failures

Ensure Java 17 is installed: java -version

Clear Maven cache: mvn clean

Login Issues

Default admin: admin / admin

Check user role assignments in database

Quiz Submission Problems

Verify all questions are answered

Check browser console for JavaScript errors

Ensure timer hasn't expired

Debug Mode
Enable detailed logging by setting:

properties
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.springframework.web=DEBUG
🚀 Deployment
Local Development
bash
mvn clean package spring-boot:run
Production Build
bash
mvn clean package -DskipTests
java -jar target/smartquizapp-0.0.1-SNAPSHOT.jar
Docker Deployment
bash
docker build -t smartquizapp .
docker run -p 8080:8080 smartquizapp
📈 Future Enhancements
Email notifications for quiz results

Question categories and tags

Advanced analytics and reporting

Question image support

Export results to PDF/Excel

REST API for mobile apps

Social features and sharing

Advanced question types (multiple correct, matching, etc.)

🤝 Contributing
Fork the repository

Create a feature branch: git checkout -b feature/new-feature

Commit changes: git commit -am 'Add new feature'

Push to branch: git push origin feature/new-feature

Submit a pull request

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

👥 Demo Accounts
Admin: admin / admin - Full access to all features

Student: student / student - Quiz participation only

Built with ❤️ using Spring Boot & Modern Web Technologies

For support or questions, please check the troubleshooting section or create an issue in the repository.

