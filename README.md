# SME-Assignment

## Part1: Setting up your Project 
Took me only 10 min to setup the project. I have made the following changes:
Copy pasted the inclde and lib in the `smfl` folder.

## Part2: Bug Fixing
Fixed the bug in the code. The bug was in following file: Took me only 20 min to fix the bug.
1. Space-Invaders/header/Gameplay/HighScore.h
	on line number 12, previously it was 
    `static class HighScore
    {
    public:
        static void saveHighScore(const HighScoreData& highScore);
        static HighScoreData loadHighScore();
    };`

    changed it to

    `class HighScore
    {
    public:
        static void saveHighScore(const HighScoreData& highScore);
        static HighScoreData loadHighScore();
    };`

    cause the static keyword was not needed during class declaration , it was overwrting the class objects.

2. Space-Invaders/header/Player/PlayerModel.h
    changed line 57 from 
   `static const int invincible_player_alpha = 170.f;`
    to
   `static const int invincible_player_alpha = 170;`
    
	cause the value was float and it was being assigned to int and it was required static.
    
3. Space-Invaders/source/Enemy/EnemyController.cpp , line 53
	changed 
	`float x_offset_distance = (std::rand() % static_cast<int>(enemy_model->right_most_position.x - enemy_model->left_most_position.x));`
	to
    `float x_offset_distance = static_cast<float>(std::rand() % static_cast<int>(enemy_model->right_most_position.x - enemy_model->left_most_position.x));	`

    cause the value was float and it was being assigned to int.

4. Space-Invaders/source/Gameplay/GameplayView.cpp , Space-Invaders/source/UI/MainMenu/MainMenuUIController.cpp

  fixed the bug in the code by changing the following line:
  `background_image->initialize(Config::background_texture_path,
			static_cast<float>(game_window->getSize().x),
			static_cast<float>(game_window->getSize().y),
			sf::Vector2f(0, 0));`

5. Space-Invaders/header/Player/PlayerView.h, Space-Invaders/header/Player/PlayerController.h

The issue i encountered was likely due to a circular dependency between PlayerController.h and PlayerView.h. To resolve this, i used forward declarations in PlayerController.h and PlayerView.h instead of including each other's headers directly. 