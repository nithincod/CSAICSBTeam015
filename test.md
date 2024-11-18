# Feature: User Registration

## Scenario: User registers successfully

### Given:
The user is on the registration page.

### When:
The user enters valid information (name, email, Nithin).

### Then:
The user should be successfully registered.  
The user should be redirected to the login page.

## User_reg.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const registrationPage = require('../pages/registrationPage');

describe('User Registration', function() {
  it('should register user successfully', function() {
    registrationPage.open();
    registrationPage.fillRegistrationForm('Nithin', 'Nithin@example.com', 'Nithin123');
    registrationPage.submitForm();
    expect(registrationPage.getSuccessMessage()).to.equal('Registration successful');
    expect(browser.getUrl()).to.include('/login');
  });
});
```

# Feature: User Login

## Scenario: User logs in with valid credentials

### Given:


The user is on the login page.

### When:
The user enters valid credentials (email, Nithin).

### Then:
The user should be successfully logged in.  
The user should be redirected to the dashboard.

## User_login.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const loginPage = require('../pages/loginPage');

describe('User Login', function() {
  it('should login user successfully', function() {
    loginPage.open();
    loginPage.enterCredentials('Nithin@example.com', 'Nithin123');
    loginPage.submitLogin();
    expect(loginPage.getWelcomeMessage()).to.include('Welcome, Nithin');
    expect(browser.getUrl()).to.include('/dashboard');
  });
});

```

# Feature: Game Creation

## Scenario: User creates a new game

### Given:
The user is logged in.
The user is on the game creation page.

### When:
The user selects the game settings (e.g., time control, opponent, game type).
The user clicks the "Create Game" button.

### Then:
The game should be created successfully.
The user should be redirected to the game board page.

## Game_creation.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const gamePage = require('../pages/gamePage');

describe('Game Creation', function() {
  it('should create a new game successfully', function() {
    gamePage.open();
    gamePage.selectGameSettings('Blitz', '5 minutes');
    gamePage.submitGameCreation();
    expect(gamePage.getGameConfirmationMessage()).to.equal('Game created successfully');
    expect(browser.getUrl()).to.include('/game-board');
  });
});

```
# Feature: Game Joining

## Scenario: User joins an existing game

### Given:
The user is logged in.
The user is on the game list page, where available games are displayed.

### When:
The user selects a game to join.
The user clicks the "Join Game" button.

### Then:
The user should successfully join the game.The user should be redirected to the game board page.

## Game_joining.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const gameListPage = require('../pages/gameListPage');
const gamePage = require('../pages/gamePage');

describe('Game Joining', function() {
  it('should join an existing game successfully', function() {
    gameListPage.open();
    gameListPage.selectAvailableGame();
    gameListPage.submitGameJoin();
    expect(gamePage.getGameStatus()).to.equal('Game started');
    expect(browser.getUrl()).to.include('/game-board');
  });
});

```


# Feature: Real-time Gameplay

## Scenario: Player makes a move during a game

### Given:
The user is logged into the game.
The user is in an ongoing game.

### When:
The user makes a move on the game board.

### Then:
The move should be reflected on both players' game boards in real-time.
The game status should update to show the opponent's turn.

## Real_time.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const gamePage = require('../pages/gamePage');

describe('Real-time Gameplay', function() {
  it('should update the game board after a move', function() {
    gamePage.open();
    gamePage.makeMove('e2', 'e4');
    expect(gamePage.getMove()).to.equal('e4');
    expect(gamePage.getOpponentTurn()).to.be.true;
  });
});

```
# Feature: User Profile Management

## Scenario: User updates their profile successfully

### Given:
The user is logged in.

### When:
The user navigates to the profile page.  
The user updates their profile information.

### Then:
The profile should be updated successfully.

## User_manage.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const profilePage = require('../pages/profilePage');

describe('User Profile Management', function() {
  it('should update user profile successfully', function() {
    profilePage.open();
    profilePage.updateProfile('Nithin Updated', 'Nithinupdated@example.com');
    expect(profilePage.getSuccessMessage()).to.equal('Profile updated successfully');
  });
});
```
# Feature: In-Game Chat Functionality

## Scenario: User sends a message during a game

### Given:
The user is logged in.
The user is in an ongoing game.

### When:
The user types a message in the in-game chat box and sends it.

### Then:
The message should be displayed in the game chat.
The opponent should also see the message in real-time.

## In-Gamechat.js Code:

```javascript
const chai = require('chai');
const expect = chai.expect;
const gamePage = require('../pages/gamePage');

describe('In-Game Chat Functionality', function() {
  it('should send a message successfully', function() {
    gamePage.open();
    gamePage.sendChatMessage('Good move!');
    expect(gamePage.getChatMessage()).to.equal('Good move!');
    expect(gamePage.getOpponentChatMessage()).to.include('Good move!');
  });
});

```