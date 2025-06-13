# Messaging Application Testing Guide

## 1. Authentication Testing

### Register User
```http
POST http://localhost:3001/api/auth/register
Content-Type: application/json

{
    "name": "Test User",
    "email": "test@example.com",
    "password": "password123"
}
```

### Login User
```http
POST http://localhost:3001/api/auth/login
Content-Type: application/json

{
    "email": "test@example.com",
    "password": "password123"
}
```
- Save the returned token for authenticated requests

## 2. Message Testing

### Send Message
```javascript
// Using Socket.IO
socket.emit('message', {
    event: 'send_message',
    data: {
        senderId: 'user_id_1',
        receiverId: 'user_id_2',
        content: 'Hello, this is a test message!'
    }
});
```

### Get Unread Messages Count
```http
GET http://localhost:3001/api/messages/unread/{userId}
Authorization: Bearer your_token_here
```

### Get Chat History
```http
GET http://localhost:3001/api/messages/{userId1}/{userId2}
Authorization: Bearer your_token_here
```

### Mark Messages as Read
```http
PUT http://localhost:3001/api/messages/read/{senderId}/{receiverId}
Authorization: Bearer your_token_here
```

## 3. Real-time Features Testing

### User Online/Offline Status
```javascript
// Login
socket.emit('user_login', {
    userId: 'user_id_here'
});

// Logout
socket.emit('user_logout', {
    userId: 'user_id_here'
});
```

### Typing Indicator
```javascript
// Start typing
socket.emit('typing', {
    senderId: 'user_id_1',
    receiverId: 'user_id_2',
    isTyping: true
});

// Stop typing
socket.emit('typing', {
    senderId: 'user_id_1',
    receiverId: 'user_id_2',
    isTyping: false
});
```

### Message Delivery Status
```javascript
// When message is delivered
socket.emit('message_delivered', {
    messageId: 'message_id_here',
    senderId: 'user_id_1',
    receiverId: 'user_id_2'
});
```

### Message Read Status
```javascript
// When message is read
socket.emit('message_read', {
    messageId: 'message_id_here',
    senderId: 'user_id_1',
    readerId: 'user_id_2'
});
```

### Message Reactions
```javascript
// Add reaction to message
socket.emit('message_reaction', {
    messageId: 'message_id_here',
    userId: 'user_id_here',
    reaction: '👍'  // or any emoji
});
```

## 4. Testing Steps

1. **Setup**
   - Start the server
   - Connect two WebSocket clients (e.g., using Postman or browser)

2. **Authentication Flow**
   - Register two users
   - Login with both users
   - Save tokens for both users

3. **Basic Messaging**
   - Send messages between users
   - Check unread message count
   - Get chat history
   - Mark messages as read

4. **Real-time Features**
   - Test online/offline status
   - Test typing indicators
   - Test message delivery status
   - Test read receipts
   - Test message reactions

5. **Error Cases**
   - Test with invalid tokens
   - Test with non-existent user IDs
   - Test with invalid message formats

## 5. Expected Results

### Message Status Flow
1. Message sent → `message_sent` event
2. Message delivered → `message_delivery_status` event
3. Message read → `message_read_status` event

### User Status Events
- `user_status_change`: When user goes online/offline
- `user_typing`: When user starts/stops typing
- `user_presence_update`: When user's presence changes

### Message Events
- `receive_message`: When new message is received
- `message_reaction_update`: When message reaction changes

## 6. Testing Tools

1. **Postman**
   - For REST API testing
   - For WebSocket testing

2. **Browser Console**
   - For testing Socket.IO events
   - For debugging real-time features

3. **MongoDB Compass**
   - For verifying message storage
   - For checking message status updates

## 7. Common Issues and Solutions

1. **Socket Connection Issues**
   - Check if server is running
   - Verify WebSocket URL
   - Check CORS settings

2. **Authentication Issues**
   - Verify token format
   - Check token expiration
   - Ensure proper Authorization header

3. **Message Delivery Issues**
   - Check user online status
   - Verify message format
   - Check database connection

4. **Real-time Feature Issues**
   - Verify Socket.IO connection
   - Check event names
   - Verify data format