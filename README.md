# Edura Server - Node.js Backend

The backend API server for Edura Learning Management System built with Node.js, Express.js, and MongoDB.

## 🚀 Features

### Authentication & Authorization

- **JWT-based Authentication**: Secure token-based authentication system
- **Role-based Access Control**: Separate permissions for students and instructors
- **Password Security**: bcrypt hashing for secure password storage
- **Session Management**: Token-based session handling

### Course Management

- **CRUD Operations**: Complete course creation, reading, updating, and deletion
- **Curriculum Management**: Video lecture organization and management
- **Course Publishing**: Publish/unpublish course functionality
- **Student Enrollment**: Track student enrollments and payments

### Media Management

- **File Upload**: Secure file upload with Multer middleware
- **Cloudinary Integration**: Cloud-based media storage and optimization
- **Video Processing**: Support for various video formats
- **Image Optimization**: Automatic image resizing and optimization

### Payment Processing

- **PayPal Integration**: Secure payment processing with PayPal SDK
- **Order Management**: Complete order lifecycle management
- **Payment Verification**: Secure payment confirmation and verification
- **Transaction Tracking**: Detailed transaction history and status

### Student Progress Tracking

- **Progress Monitoring**: Track student learning progress
- **Completion Tracking**: Monitor course completion rates
- **Analytics**: Provide insights into student engagement
- **Performance Metrics**: Detailed learning analytics

## 🛠️ Tech Stack

- **Node.js** - JavaScript runtime environment
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **JWT** - JSON Web Tokens for authentication
- **bcryptjs** - Password hashing and verification
- **Multer** - File upload middleware
- **Cloudinary** - Cloud media storage service
- **PayPal SDK** - Payment processing integration
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variable management

## 📁 Project Structure

```
server/
├── controllers/           # Request handlers and business logic
│   ├── auth-controller/   # Authentication operations
│   ├── instructor-controller/ # Instructor-specific operations
│   └── student-controller/    # Student-specific operations
├── helpers/              # Utility functions and external integrations
│   ├── cloudinary.js     # Cloudinary configuration and helpers
│   └── paypal.js         # PayPal integration helpers
├── middleware/           # Custom middleware functions
│   └── auth-middleware.js # Authentication and authorization middleware
├── models/              # MongoDB schemas and models
│   ├── Course.js        # Course data model
│   ├── CourseProgress.js # Student progress tracking model
│   ├── Order.js         # Payment order model
│   ├── StudentCourses.js # Student-course relationship model
│   └── User.js          # User authentication model
├── routes/              # API route definitions
│   ├── auth-routes/     # Authentication endpoints
│   ├── instructor-routes/ # Instructor-specific endpoints
│   └── student-routes/  # Student-specific endpoints
├── server.js           # Main application entry point
├── package.json        # Dependencies and scripts
└── .env               # Environment variables (create this file)
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v16 or higher)
- MongoDB (local or cloud instance)
- PayPal Developer Account
- Cloudinary Account

### Installation

1. **Navigate to the server directory**

   ```bash
   cd server
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Environment Setup**

   Create a `.env` file in the server directory:

   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/edura_lms
   JWT_SECRET=your_super_secret_jwt_key_here
   CLIENT_URL=http://localhost:5173
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   PAYPAL_CLIENT_ID=your_paypal_client_id
   PAYPAL_CLIENT_SECRET=your_paypal_client_secret
   ```

4. **Start the development server**

   ```bash
   npm run dev
   ```

5. **Access the API**
   - API Base URL: http://localhost:5000
   - Health Check: http://localhost:5000/health

### Available Scripts

- `npm run dev` - Start development server with nodemon
- `npm start` - Start production server
- `npm test` - Run tests (if configured)

## 📚 API Endpoints

### Authentication Routes (`/auth`)

- `POST /auth/signup` - User registration
- `POST /auth/signin` - User login
- `POST /auth/verify` - Verify JWT token

### Instructor Routes (`/instructor/course`)

- `GET /instructor/course` - Get instructor's courses
- `POST /instructor/course` - Create new course
- `PUT /instructor/course/:id` - Update course
- `DELETE /instructor/course/:id` - Delete course
- `GET /instructor/course/:id` - Get specific course details

### Media Routes (`/media`)

- `POST /media/upload` - Upload media files (images/videos)
- `DELETE /media/:public_id` - Delete media files

### Student Routes (`/student`)

- `GET /student/course` - Get available courses
- `GET /student/course/:id` - Get course details
- `POST /student/order` - Create payment order
- `GET /student/courses-bought` - Get purchased courses
- `POST /student/course-progress` - Update course progress
- `GET /student/course-progress/:id` - Get course progress

## 🗄️ Database Models

### User Model

```javascript
{
  userName: String,
  userEmail: String,
  password: String,
  role: String // 'student' or 'instructor'
}
```

### Course Model

```javascript
{
  instructorId: String,
  instructorName: String,
  title: String,
  category: String,
  level: String,
  primaryLanguage: String,
  subtitle: String,
  description: String,
  image: String,
  welcomeMessage: String,
  pricing: Number,
  objectives: String,
  students: [{
    studentId: String,
    studentName: String,
    studentEmail: String,
    paidAmount: String
  }],
  curriculum: [{
    title: String,
    videoUrl: String,
    public_id: String,
    freePreview: Boolean
  }],
  isPublised: Boolean
}
```

### CourseProgress Model

```javascript
{
  courseId: String,
  studentId: String,
  completedLectures: [String],
  progressPercentage: Number,
  lastAccessedAt: Date
}
```

### Order Model

```javascript
{
  courseId: String,
  studentId: String,
  amount: Number,
  currency: String,
  paymentId: String,
  status: String,
  createdAt: Date
}
```

## 🔒 Security Features

### Authentication & Authorization

- JWT token validation
- Role-based access control
- Password hashing with bcrypt
- Secure session management

### Data Protection

- Input validation and sanitization
- SQL injection prevention (MongoDB)
- XSS protection
- CORS configuration

### File Upload Security

- File type validation
- File size limits
- Secure file storage with Cloudinary
- Virus scanning (if configured)

## 🔧 Configuration

### Environment Variables

All configuration is handled through environment variables:

- **PORT** - Server port (default: 5000)
- **MONGO_URI** - MongoDB connection string
- **JWT_SECRET** - Secret key for JWT tokens
- **CLIENT_URL** - Frontend application URL
- **CLOUDINARY\_\*** - Cloudinary configuration
- **PAYPAL\_\*** - PayPal API credentials

### Database Configuration

- MongoDB connection with Mongoose
- Connection pooling
- Error handling and reconnection
- Index optimization

### CORS Configuration

```javascript
cors({
  origin: process.env.CLIENT_URL,
  methods: ["GET", "POST", "DELETE", "PUT"],
  allowedHeaders: ["Content-Type", "Authorization"],
});
```

## 🚀 Deployment

### Production Setup

1. Set production environment variables
2. Configure MongoDB Atlas or production database
3. Set up Cloudinary production account
4. Configure PayPal production credentials

### Deployment Options

- **Heroku** - Easy deployment with Git integration
- **AWS EC2** - Scalable cloud deployment
- **DigitalOcean** - VPS deployment
- **Railway** - Modern deployment platform
- **Render** - Simple deployment service

### Environment Variables for Production

```env
NODE_ENV=production
PORT=5000
MONGO_URI=your_production_mongodb_uri
JWT_SECRET=your_production_jwt_secret
CLIENT_URL=https://your-frontend-domain.com
CLOUDINARY_CLOUD_NAME=your_production_cloudinary_name
CLOUDINARY_API_KEY=your_production_cloudinary_key
CLOUDINARY_API_SECRET=your_production_cloudinary_secret
PAYPAL_CLIENT_ID=your_production_paypal_client_id
PAYPAL_CLIENT_SECRET=your_production_paypal_client_secret
```

## 🧪 Testing

### API Testing

- Use Postman or similar tools for API testing
- Test all endpoints with proper authentication
- Verify error handling and validation

### Database Testing

- Test database connections
- Verify data integrity
- Test backup and recovery procedures

## 📊 Monitoring & Logging

### Error Handling

- Centralized error handling middleware
- Detailed error logging
- User-friendly error messages

### Performance Monitoring

- Request/response logging
- Database query optimization
- Memory usage monitoring

## 🤝 Contributing

1. Follow Node.js best practices
2. Use proper error handling
3. Write meaningful commit messages
4. Test your changes thoroughly
5. Update documentation as needed

## 📝 License

This project is licensed under the ISC License.

## 🔗 External Services

### Cloudinary

- Cloud-based media storage
- Automatic image/video optimization
- CDN delivery
- Secure upload URLs

### PayPal

- Secure payment processing
- Multiple payment methods
- Transaction tracking
- Webhook notifications

### MongoDB Atlas

- Cloud database hosting
- Automatic backups
- Scalability
- Security features

---

**Edura Server** - Robust Node.js backend for the Learning Management System
