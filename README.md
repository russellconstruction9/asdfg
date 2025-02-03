<!DOCTYPE html>
<html>
<head>
    <title>Chatbot</title>
    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        #chatbox { border: 1px solid #ccc; padding: 10px; width: 500px; height: 400px; overflow-y: scroll; }
        .message { margin: 5px 0; }
        .user { color: blue; }
        .bot { color: green; }
    </style>
</head>
<body>
    <h2>Simple Chatbot</h2>
    <div id="chatbox"></div>
    <input type="text" id="user_input" placeholder="Type your message here..." style="width:400px;">
    <button id="send_btn">Send</button>

    <script>
        $(document).ready(function(){
            $("#send_btn").on("click", function(){
                var userText = $("#user_input").val();
                if(userText === "") return;
                $("#chatbox").append("<div class='message user'><strong>You:</strong> " + userText + "</div>");
                $.post("/get", { msg: userText }, function(data){
                    $("#chatbox").append("<div class='message bot'><strong>Bot:</strong> " + data + "</div>");
                    $("#chatbox").scrollTop($("#chatbox")[0].scrollHeight);
                });
                $("#user_input").val("");
            });

            // Allow Enter key to send the message
            $("#user_input").keypress(function(e){
                if(e.which == 13){
                    $("#send_btn").click();
                }
            });
        });
    </script>
</body>
</html>
