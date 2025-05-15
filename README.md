## a. How much data does the publisher program send to the message broker in one run?**  
In one run, the publisher calls `publish_event` five times. Each call sends one AMQP message, totaling **5 messages**. Each message contains a Borsh-serialized `UserCreatedEventMessage`, which includes fields such as user ID, name, and email. While the exact size depends on the content and serialization, the message count is consistently five per run.

## b. What does the URL `amqp://guest:guest@localhost:5672` mean, and why is it the same in both publisher and subscriber programs?**  
This URL is the AMQP connection string used to access the RabbitMQ broker:

- `amqp://` — specifies the protocol (AMQP)
- `guest:guest` — username and password (default credentials)
- `localhost` — the broker is hosted on the local machine
- `5672` — the default TCP port for AMQP

By using the same URL in both the publisher and subscriber programs, both are connecting to the same RabbitMQ instance. This allows the publisher to send messages into exchanges/queues on the broker, and the subscriber to consume those messages from the same location.


<img width="1280" alt="running_rabbitmq" src="https://github.com/user-attachments/assets/9f7a7888-223b-4dcc-a556-f98842f9785e" />

</br>

<img width="1267" alt="Image" src="https://github.com/user-attachments/assets/5bfc54e6-a8b0-4265-9797-d5463a016bdc" />

In this image, we can see the interaction between a Publisher and a Subscriber program using a message broker, which is RabbitMQ. When both the Publisher and Subscriber are executed (cargo run), the Publisher sends user data as messages to the message broker, and the Subscriber listens for these messages and receives them. The terminal on the right shows that the Publisher executed successfully, while the terminal on the left confirms that the Subscriber received the UserCreatedEventMessage multiple times, each containing user data such as ID and username. This demonstrates a successful message-passing mechanism: the Publisher sends data, and the Subscriber captures and prints each message upon arrival.