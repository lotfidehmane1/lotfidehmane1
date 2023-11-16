import android.app.Activity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import org.telegram.telegrambots.ApiContextInitializer;
import org.telegram.telegrambots.TelegramBotsApi;
import org.telegram.telegrambots.exceptions.TelegramApiException;
import org.telegram.telegrambots.generics.BotSession;
import org.telegram.telegrambots.meta.TelegramBotsApi;
import org.telegram.telegrambots.meta.api.methods.send.SendMessage;
import org.telegram.telegrambots.meta.api.objects.Message;
import org.telegram.telegrambots.meta.api.objects.Update;
import org.telegram.telegrambots.meta.exceptions.TelegramApiRequestException;

import java.io.Serializable;

public class MainActivity extends Activity {
    EditText etInput;
    Button btnSend;
    TelegramBotsApi telegramBotsApi;
    SendBot sendBot;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ApiContextInitializer.init();

        etInput = findViewById(R.id.etInput);
        btnSend = findViewById(R.id.btnSend);

        telegramBotsApi = new TelegramBotsApi();
        sendBot = new SendBot();

        try {
            telegramBotsApi.registerBot(sendBot);
        } catch (TelegramApiException e) {
            e.printStackTrace();
        }

        btnSend.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String message = etInput.getText().toString();
                SendMessage sendMessage = new SendMessage();
                sendMessage.setChatId("@YourChannelOrGroupUsername
                
