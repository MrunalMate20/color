1. HTML Structure

    The <html> element defines the root of the document.
    The <head> element contains metadata and links for external fonts, stylesheets, and the document's title.
    The <body> contains the structure and layout for the game, including the header, score display, timer, game canvas, and finished message.

2. External Resources

    Google Fonts: The Roboto font is loaded using the link <link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">.
    Animate.css: This library is loaded to add animations to elements (bounce, tada) with the link <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/animate.css@3.5.2/animate.min.css">.

3. CSS Styles

    The CSS styles are defined in the <style> section to control the visual layout of the page.
    body styles:
        A linear gradient background is set to shift from dark gray to light blue (linear-gradient(0deg, rgba(52, 52, 50, 1) 0%, rgba(74, 143, 164, 1) 100%)).
        The Roboto font is applied to the entire body.
    .container: Centers the game elements using Flexbox.
    #canvas:
        Uses CSS Grid to arrange 3 columns of cards (grid-template-columns: repeat(3, 100px)).
        Each card is styled as a 100px x 100px square with a gap of 10px between cards (grid-gap: 10px).
    .card:
        Default color (#ddd), with hidden text (transparent), a border, and rounded corners.
        A hover effect is implied with cursor: pointer.
    .matched: Indicates matched cards with a green background and white text.
    .flipped: Cards that are currently flipped show their color and black text.
    #finished: This is a hidden div that appears after the game ends, showing the final score and a reset button.

4. jQuery Script

The main logic for the game is handled with jQuery in the <script> section, which executes once the page is fully loaded:
a) Game Variables

    colors: An array of six colors.
    cardValues: Contains two sets of each color (to create 12 cards, i.e., 6 pairs).
    score: Tracks the number of successful matches.
    timerDuration: 30 seconds for the countdown timer.
    timer: Stores the interval for the countdown.
    firstCard, secondCard: Store the two cards being flipped.
    lockBoard: Prevents multiple cards from being clicked during certain operations (e.g., waiting for a mismatch).

b) Shuffling Function

    shuffle(array): A function to randomly shuffle the colors in cardValues using the Fisher-Yates algorithm.

c) Card Creation

    createCards():
        Shuffles cardValues.
        Loops through the shuffled array to create 12 cards dynamically using jQuery.
        Each card is created as a <div> with a data-color attribute storing its color and appended to the #canvas div.

d) Game Start

    startGame():
        Initializes the score and timer on the screen.
        Hides the finished screen.
        Calls createCards() to generate the cards.
        Starts a countdown timer (setInterval) that decreases every second, updating the displayed timer.
        Ends the game when the timer reaches zero.

e) Card Click Handling

    When a card is clicked:
        If the card is already flipped, matched, or if the board is locked, no action is taken.
        Otherwise, the card is flipped (its background color is revealed, and the text color changes).
        The first clicked card is stored in firstCard, and the second one in secondCard.
    If two cards are flipped, the program checks:
        If their data-color matches:
            Both cards are marked as matched, and the score is incremented.
        If they do not match:
            A short delay (1 second) occurs before the cards are flipped back to their default state (gray color).
    The board is locked (lockBoard = true) while the second card is flipped to prevent interference, and then unlocked after the match check.
    
