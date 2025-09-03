<!DOCTYPE html>
updateCard();
}


function speakWord() {
const utterance = new SpeechSynthesisUtterance(numbers[currentIndex].word);
utterance.lang = "en-US";
speechSynthesis.speak(utterance);
}


// Quiz
function startQuiz() {
currentQuiz = numbers[Math.floor(Math.random() * numbers.length)];
document.getElementById("quiz-question").innerText = `Które słowo oznacza liczbę ${currentQuiz.num}?`;
document.getElementById("quiz-sound").style.display = "inline-block";


let options = [currentQuiz.word];
while (options.length < 3) {
const opt = numbers[Math.floor(Math.random() * numbers.length)].word;
if (!options.includes(opt)) options.push(opt);
}
options.sort(() => Math.random() - 0.5);


const container = document.getElementById("quiz-options");
container.innerHTML = "";
options.forEach(opt => {
const btn = document.createElement("button");
btn.innerText = opt;
btn.className = "quiz-btn";
btn.onclick = () => checkAnswer(opt, currentQuiz.word);
container.appendChild(btn);
});
}


function checkAnswer(chosen, correct) {
const feedback = document.getElementById("quiz-feedback");
if (chosen === correct) {
feedback.innerText = "✅ Brawo! Dobra odpowiedź.";
} else {
feedback.innerText = `❌ To nie to. Poprawnie: ${correct}`;
}
setTimeout(startQuiz, 2000);
}


function speakQuizNumber() {
if (currentQuiz) {
const utterance = new SpeechSynthesisUtterance(currentQuiz.word);
utterance.lang = "en-US";
speechSynthesis.speak(utterance);
}
}


// Start
updateCard();
startQuiz();
</script>
</body>
</html>
