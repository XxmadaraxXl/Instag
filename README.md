# Instag
#include <iostream>
#include <vector>

class User {
public:
    std::string username;
    std::string email;
    std::string password;

    User(const std::string& username, const std::string& email, const std::string& password)
        : username(username), email(email), password(password) {}
};

class Post {
public:
    std::string caption;
    std::string imageUrl;
    int likes;

    Post(const std::string& caption, const std::string& imageUrl)
        : caption(caption), imageUrl(imageUrl), likes(0) {}
};

class InstagramApp {
private:
    std::vector<User> users;
    std::vector<Post> posts;
    User* currentUser;

public:
    InstagramApp() : currentUser(nullptr) {}

    void registerUser(const std::string& username, const std::string& email, const std::string& password) {
        users.push_back(User(username, email, password));
        std::cout << "User registered successfully!" << std::endl;
    }

    bool loginUser(const std::string& email, const std::string& password) {
        for (User& user : users) {
            if (user.email == email && user.password == password) {
                currentUser = &user;
                std::cout << "User logged in successfully!" << std::endl;
                return true;
            }
        }
        std::cout << "Invalid email or password. Login failed." << std::endl;
        return false;
    }

    void logoutUser() {
        currentUser = nullptr;
        std::cout << "User logged out successfully!" << std::endl;
    }

    void createPost(const std::string& caption, const std::string& imageUrl) {
        if (currentUser == nullptr) {
            std::cout << "Please login to create a post." << std::endl;
            return;
        }

        posts.push_back(Post(caption, imageUrl));
        std::cout << "Post created successfully!" << std::endl;
    }

    void likePost(Post& post) {
        if (currentUser == nullptr) {
            std::cout << "Please login to like a post." << std::endl;
            return;
        }

        post.likes++;
        std::cout << "Post liked!" << std::endl;
    }
};

int
