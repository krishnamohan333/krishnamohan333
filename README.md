- 👋 Hi, I’m @krishnamohan333
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
krishnamohan333/krishnamohan333 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
public class Main {
    
}
import java.util.*;

class ChatUser {
    private String username;
    private List<String> messages;

    public ChatUser(String username) {
        this.username = username;
        this.messages = new ArrayList<>();
    }

    public String getUsername() {
        return username;
    }

    public List<String> getMessages() {
        return messages;
    }

    public void sendMessage(String message, ChatRoom chatRoom) {
        chatRoom.sendMessage(this, message);
    }

    public void receiveMessage(String message) {
        messages.add(message);
    }
}

class ChatRoom {
    private List<ChatUser> users;

    public ChatRoom() {
        users = new ArrayList<>();
    }

    public void addUser(ChatUser user) {
        users.add(user);
    }

    public void sendMessage(ChatUser sender, String message) {
        for (ChatUser user : users) {
            if (!user.equals(sender)) {
                user.receiveMessage(sender.getUsername() + ": " + message);
            }
        }
    }
}

public class ChatApplication {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        ChatRoom chatRoom = new ChatRoom();

        System.out.println("Welcome to the Chat Application!");

        System.out.print("Enter your username: ");
        String username = scanner.nextLine();

        ChatUser currentUser = new ChatUser(username);
        chatRoom.addUser(currentUser);

        System.out.println("You joined the chat room. Start chatting!");

        while (true) {
            System.out.print("> ");
            String message = scanner.nextLine();

            if (message.equalsIgnoreCase("exit")) {
                System.out.println("Goodbye!");
                break;
            }

            currentUser.sendMessage(message, chatRoom);
        }

        scanner.close();
    }
}
