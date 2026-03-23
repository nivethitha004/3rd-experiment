package com.example.rekha;

import android.media.MediaPlayer;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    Button btnPlay, btnNext, btnPrev;
    TextView songTitle;

    MediaPlayer mediaPlayer;

    int currentSong = 0;

    int[] songs = {R.raw.song1, R.raw.song2};
    String[] songNames = {"Song 1", "Song 2"};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnPlay = findViewById(R.id.btnPlay);
        btnNext = findViewById(R.id.btnNext);
        btnPrev = findViewById(R.id.btnPrev);
        songTitle = findViewById(R.id.songTitle);

        playSong(currentSong);

        // Play / Pause
        btnPlay.setOnClickListener(v -> {
            if (mediaPlayer != null && mediaPlayer.isPlaying()) {
                mediaPlayer.pause();
                btnPlay.setText("▶");
            } else {
                mediaPlayer.start();
                btnPlay.setText("⏸");
            }
        });

        // Next
        btnNext.setOnClickListener(v -> {
            currentSong = (currentSong + 1) % songs.length;
            playSong(currentSong);
        });

        // Previous
        btnPrev.setOnClickListener(v -> {
            currentSong = (currentSong - 1 + songs.length) % songs.length;
            playSong(currentSong);
        });
    }

    private void playSong(int songIndex) {

        if (mediaPlayer != null) {
            mediaPlayer.release();
        }

        mediaPlayer = MediaPlayer.create(this, songs[songIndex]);
        songTitle.setText(songNames[songIndex]);
        mediaPlayer.start();
        btnPlay.setText("⏸");

        // Auto play next song after completion
        mediaPlayer.setOnCompletionListener(mp -> {
            currentSong = (currentSong + 1) % songs.length;
            playSong(currentSong);
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (mediaPlayer != null) {
            mediaPlayer.release();
            mediaPlayer = null;
        }
    }
}
