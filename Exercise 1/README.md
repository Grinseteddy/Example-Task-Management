# Excercise 1: Discussion Data Exchange

We have a [context map](https://miro.com/app/board/uXjVNX-5o1M=/?moveToWidget=3458764567650869937&cot=14).

1. Let us discuss which data needs to be exchanged.
   We mark the according data flow with the data to be exchanged using the aggregates out of the event storming.
   We discuss if we need to provide or consume the data asynchronously or synchronously. The arrows are dashed or lined.
   [Possible solution](https://miro.com/app/board/uXjVNX-5o1M=/?moveToWidget=3458764567771317676&cot=14)
2. We discuss for each synchronous arrow (using REST), which http verb should be used. We can use a color coding for it
   (e.g., Post yellow, Put green, and Get blue).
   [Possible solution](https://miro.com/app/board/uXjVNX-5o1M=/?moveToWidget=3458764568517446347&cot=14)
3. We discuss the asynchronous arrows (using Kafka), which business event triggers the data exchange, and we name the
   card accordingly. We discuss if we want to use a full state event (yellow), a delta event (green), or just a
   notification event (blue). We mark them via color coding as well.
   [Possible solution](https://miro.com/app/board/uXjVNX-5o1M=/?moveToWidget=3458764568517446347&cot=14)**