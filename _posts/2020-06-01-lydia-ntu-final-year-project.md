---
title: '[NTU FYP] Lydia: A Horror Adventure Story'
date: 2020-06-01
---


![Banner](/assets/imgs/lydia/lydia.png)

This is a reflection of my Final Year Project at NTU. Instead of finishing with a complete game product as I initially expected, it was more of a series of experiments with different technical aspects in game development. Nevertheless, It helped me grow as a game developer and learn from my own trials and errors.

My love affair with horror games began as my first play-through of Silent Hill 2. It was in my second year of college. I finally got tired of all the competitive action shooter game (Overwatch, Rainbow 6 Seige, CSGO etc.) at the time while starting to develop a taste for the “classic” games. And although there were certainly lots of titles that have later become the major inspirations for the industry, the only one that I weirdly fall in love with, is the Silent Hill series.

![2D Prototype](/assets/imgs/lydia/Screenshot-2020-01-20-at-4.02.20-PM.png "2D Prototype")
_Figure 1. The initial 2D game, an extension from our previous game, The Decameron_

Another part of the story is that I have already had the experience of developing a horror game in Shanghai Taptap Game Jam. The theme was “bonfire”, and the name of our game is The Decameron. While initially, I tried to continue with the story and aesthetics of our previous 2D mobile game (Figure 1), I ended up scratching that idea completely and went on with a 3D first-person game. There are many reasons for this change. The more personal one for me, or other gamers like me, is because of the attraction of navigating in a simulated and imaginary 3D space. As I was writing my FYP report, I made the following table (Figure 2) reflecting my opinion at that time on the different experiences that different “point-of-view (POV)” can bring about in horror games.

| Point of View                           | Dimension | General Gameplay | General Immersiveness | Example                         |
|-----------------------------------------|-----------|------------------|-----------------------|---------------------------------|
| First Person                            | 3D        | Action           | High                  | Outlast                         |
| Third Person (Fixed Camera)             | 3D        | Action Puzzle    | Medium                | Resident Evil, Silent Hill      |
| Third Person (Camera Over the shoulder) | 3D        | Action           | High                  | The Last of Us, The Evil Within |
| Virtual Reality                         | 3D        | Puzzle           | Very High             | Resident Evil 7                 |
| Side-scroller                           | 2D/3D     | Puzzle           | Low                   | Detention                       |
| Top-down                                | 2D/3D     | Action           | Medium                | The Witch's House, Darkwoods    |

_Figure 2. Comparing Different POVs_

### Prototypes

The followings are several prototypes of the game. All were rendered and recorded in Unity 3D in real-time.

![3D Prototype](/assets/imgs/lydia/Screenshot-2019-11-10-at-10.20.59-AM.png "3D Prototype")
_Figure 3. Bonfire 3D_

I made the previous 2D game into 3D with a bonfire and the forest (Figure 3). The idea was similar: the player needs to find items in the dark forest while returning to the bonfire for recovery of health. Some additional gameplay elements were added: The player can “fight” the monster by “breathing” (Figure 4; the monster is Fantasy Monster; inspired by Anxiety Attack by Alessandro “NeatWolf” Salvati); The found item will appear on the cross.

![Combat](/assets/imgs/lydia/Screenshot-2020-01-13-at-10.29.13-AM.png "Combat")
_Figure 4. Combat_

Another prototype was an exploration of gameplay mechanics. I also targeted the interaction to the mobile platform but there were some optimization issues with the animation system at the time.

The mechanics are as follows: Walking into the black monolith will transform the environment into “night” (Figure 6) while the white monolith will transform the environment into “day;” (Figure 5) The monster and the key items only appear in the night, while the player needs to find the white monolith to travel back to the day to return the item; The monster can be temporarily disabled by the torch fire (Figure 7); The player needs to replenish the fire by finding the fire source in the dark forest after attacking.

![Day Forest](/assets/imgs/lydia/Prot_2_1.jpeg "Day Forest")
_Figure 5. Forest, the day, and the black monolith._

![Night Forest](/assets/imgs/lydia/Prot_2_2.jpeg "Night Forest")
_Figure 6. Forest, the night, and the white monolith._

![Monster](/assets/imgs/lydia/prot_2_3.jpeg "Monster")
_Figure 7. The monster approaching_

Regretfully, none of these was made into the final product of my FYP project. At that time I was very not sure about my ideas about this game: how to tell the story; if the mechanics are valid; if people are going to like it, etc. Reflecting on my FYP journey, I think that I should continue to explore one of these previous ideas. Maybe all I should do was take a mental break and look at them from a fresh perspective. Instead, in reality, I restarted the project by redesigning and redeveloping a new environment.

### The Final Game

#### Story

The backstory focuses on the theme of “muted”. The protagonist, Lois, lost her voice due to a car accident at a very early age. Although the family took good care of her, including her younger twin sister, Lydia, she felt like being treated unfairly at school and suffered from the fact that she cannot express anything, even to her loved ones. Lois envies her younger sister for being a “superstar” in their school. The mystery happened when the family moved into a holiday hotel, “the Church Hotel”, to celebrate the sisters’ 16th birthday. Unfortunately, Lydia went missing on the first night of their arrival. The family spent the whole holiday looking for her but found nothing. The family was doomed after the accident. Their mother went crazy and was sent to the hospital. Lois managed to forget about her younger sister. However, after the death of their father due to lung cancer, Lois received a message, calling her to go back to the hotel.

![Opening](/assets/imgs/lydia/image-3.png "Opening")
_Figure 8. Screenshot of the opening scene._

{% include embed/youtube.html id='8okGJZzr3ug' %}

#### Visual and Level

The design of the environment of the Church Hotel was inspired by the structure of NTU Hall of Residence 3, which was built by the slope of the mountain. There are three main blocks: the west hotel, the east hotel and the church. 

![Outside](/assets/imgs/lydia/outside.png "Outside")
_Figure 9. The environment from the Outside_

![Hallway](/assets/imgs/lydia/hallway.png "Hallway")
_Figure 10. The hallway_

![Hall](/assets/imgs/lydia/hall.png "Hall")

![Concierge](/assets/imgs/lydia/start1.png "Concierge")

![Hanging Light](/assets/imgs/lydia/start2.png "Hanging Light")
_Figure 11. Some other real-time rendered images_

Unity optimizes real-time performance by “baking” (a term in computer graphics, meaning building the lighting into the geometry offline, to improve the real-time performance). There are three build-in tools for baking: occlusion culling, reflection probe and global illumination (GI).

Baking the occlusion culling drastically reduces the draw-call each frame. The occlusion culling is calculated based on all the static “occluder” and “occludee” in the environment. The program is supplied with the size of the smallest occlude and smallest hole, and the backface threshold. Suitable parameters need to be chosen for better optimization.

The reflection probe acts like a 360-degree camera that captures the environment around it. Then it will project the environment onto all objects with glossy surfaces in a certain range. The reflection probe can be real-time, updated with scripts or baked. Baked reflection probe was chosen for this case for better performance.

Unity provides both real-time GI and baked GI for a more realistic environment. GI simulates light bounces by path tracing and generates lightmaps for each static object. The baking process normally takes 2-3 hours on CPU (AMD Ryzen 3700X) and 15 minutes on GPU (Nvidia RTX 2070 super), and the result is not always desirable. Therefore, GPU lightmapper is always preferred for faster debugging and iteration. However, since GPU lightmapper in Unity is still in preview, it frequently crashes and sometimes falls back to CPU lightmapper. It is normally due to the fact that the quality required for the lighmap is too high. In my experience, decreasing the lightmap size will solve the problem. Furthermore, Unity 2019 provides Optix denoiser, which is worth turning on for its capability of resolving small lighting artefacts automatically. In addition, light probes were used to sample the lighting information for the small props in the scene that do not fit into the baked lightmap.

The baking process can sometimes be extremely frustrating. Several hours or even several days can be spent on this process and nothing works. Fortunately, Unity has great community support that provides many tutorials on this topic, which helped me a lot in the process. It is really worth it when finally my game can operate in 60 fps on a rather low-end laptop.

#### Conception of the Gameplay

The gameplay focuses on the room-by-room puzzle, like traditional horror games. However, it emphasizes less on inventory management and fighting. The combat is replaced with evasive action. It is about a “triangular relationship” among the cat, the rats and the monster. The monster will always try to kill the player. The rats will block the monster from the player, but also block the way of the player. They can be, however, scared away by the cat and attracted by rotten food. The cat is an object that the player needs to carry with hands. In the meantime, the player cannot carry other objects with the cat on hand. Figure 12 summarize all the in-game characters.

| In-game Characters    | Background                                                          | Gameplay Function                |
|-----------------------|---------------------------------------------------------------------|----------------------------------|
| Lois, the protagonist | Looking for her younger sister, Lydia, in the abandoned hotel.      | The player-controlled character  |
| Crimson, the cat      | A friend of Lydia and Lois. It went missing together with Lydia six years ago.    | The cat can be used to drive the infected rats away |
| Eduardo, the monster  | The hotel owner who was transformed into a monster after the hotel was abandoned. He is obsessed with keeping the secret of the hotel. | He patrols along the hallway. He will chase and kill the player when the player is spotted. However, he can be blocked by the infected rats. |
| The infected rats     | After the hotel was abandoned, it was taken over by the rats. The rats became infected and aggressive after eating the rotten food in the hotel. | The rats normally appear in the hallway of the hotel. It will block the way. The player needs to utilize the cat or the rotten food to pass the rats. She also needs to utilize the rats to block the monster. |

_Figure 12. In-game characters_

#### Gameplay Pillars

The gameplay has five pillars: puzzle, evasive action, event, mystery, and progress tracking.

1. The **puzzle** is the main content of the game. Within the limited mechanics, different puzzles were implemented to make sure the game is engaging. The difficulty level of the puzzle also increases according to the level. Solving the puzzle requires the player to manage his hand-held object cleverly and use limited resources such as the rotten food in the right place. The doors in this game can only be unlocked manually. The player needs to select the correct key from a keychain (Figure 13) to unlock the corresponding door. There are in-game hints that help the player match the key and the lock, such as the patterns on the door and the shape of the key etc.
2. **Evasive action** happens in the fixed locations. Normally, since the monster moves very fast, the player will be caught instantly when spotted. However, the player can hide inside an elevator or a hotel room. The player needs to utilize the rats to block the monster. Noted that later in the game, the player also has the choice to kill the monster with a flamethrower, but that will be the final puzzle and the game will end after that.
3. **Events** include certain jump scares, enemy encounters, and deaths that will change the dynamics of the game. These are the “surprise” elements of the game. For example, the room that normally does not have monsters may start spawning monsters because the wall is suddenly broken.
4. **Mysteries** push forward the progress of the story, but do not change the dynamics of the game. This includes triggers for pop-up text and cutscenes and some in-game notes.
5. **Progress** of the game is shown by unlocking the three books in the church. The fire in the lamp will be blown off when the book is unlocked, and a key will appear inside the book. The game will also be autosaved on these occasions.

![Key 1](/assets/imgs/lydia/key1.png "Key 1")

![Key 2](/assets/imgs/lydia/key2.png "Key 2")
_Figure 13. Key and lock_

![3F](/assets/imgs/lydia/3f_map_detail.jpg "3F")
_Figure 14. Map of level 3_

![4F](/assets/imgs/lydia/4f_map_detail.jpg "4F")
_Figure 15. Map of level 4_

![Flowchart](/assets/imgs/lydia/Copy-of-English-copy-of-gameplay-1.png "Flowchart")
_Figure 16. Gameplay flowchart_

#### Music and Sound Design

Sound is a powerful tool to create the atmosphere in the game. Inspired by the sound design of Silent Hill series by the Japanese composer Akira Yamaoka, in the project, I also experimented on creating and composing my own sound effects and music.

The SFX that I used for the menu is a shortened and reversed church bell sound, and the Quit or Cancel button is attached to a heavy piano strumming. These sound effects intend to add a mysterious colour to the game right from the beginning.

{% include embed/audio.html src="/assets/audio/ButtonClick.wav" %}
{% include embed/audio.html src="/assets/audio/exit.wav" %}

The background music (BGM) in the menu is created in FL-studio with the analogue piano sound. It was named “Hide-and-Seek”. The music is purposefully bouncy and snatchy, analogous to the process of “hiding”, and each paragraph stops with the same heavy piano strumming as the exit sound effect, analogous to “found”. It tells the story of a monster playing a hide-and-seek game with its preys.

{% include embed/audio.html src="/assets/audio/menubg_mod1.wav" %}

In the opening cutscene, the first BGM is a piece of royalty-free music created by PSOVOD. The second BGM is created by me with Bosca Ceoil, 8-bit music composing software, and Audacity, an audio-processing software. It was named “Faith”. The first piece is played with piano while the second one is synthetic sound. The contrast of the two emphasizes the theme and the title of the game.

{% include embed/audio.html src="/assets/audio/melody_song_loop_extended.wav" %}

The SFX that plays together with the pop-up text is created in FL-studio. The BGM when the protagonist first wakes up is called “Headache”. It was inspired by a song called “The Ballad of The Broken Birdie Records” by an Icelandic post-rock band, Mum. It is created in FL-studio with the intent of showing the broken mind.

{% include embed/audio.html src="/assets/audio/headache.wav" %}

{% include embed/youtube.html id='M3G2WWfkxI' %}

### Conclusion

This project is selected as a finalist of the EEE FYP competition 2020. The judge commented that the game was impressive and reflected a lot of effort put in.

A Singapore indie game studio, Daylight studio, expressed interest in this game at an earlier stage of development. They were willing to publish the game if the game was polished for commercialization. I am really grateful for their interests and valuable suggestions.

The game was well-received by the audience. 11 of my peers or senior NTU students were asked to test the game. Most of them have expressed interest in the story and wanted to see more development in the story. Five of them have found the graphics very impressive and realistic. However, they also found the gameplay was lacking feedback. Specifically, the book unlocking mechanics were a bit arbitrary and did not make sense to them.

I am really thankful for the supervision of Dr Wesley Tan Chee Wah and Asst Prof Elke Reinhuber. They offered me great freedom and respect for my own exploration and decision-making, closely followed my progress and gave me great support throughout the project.

Game development is often a multi-disciplinary task and complex by its nature. I learnt through this project that although a great game idea is tested with repeated prototyping and iterations, it is equally important to stick to one idea and just make the game complete in the first place. One thing that I am happy with when I reflect on my journey is that I kept very detailed documentation throughout the project. With this, I am able to visit my past from a new perspective. It has been an interesting visit, and it can help me re-orient myself in my current adventure.

