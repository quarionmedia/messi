import { useState, useEffect } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

export default function MessiQuiz() {
  const [quiz, setQuiz] = useState([]);
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [gameOver, setGameOver] = useState(false);

  useEffect(() => {
    fetch("https://en.wikipedia.org/api/rest_v1/page/summary/Lionel_Messi")
      .then((res) => res.json())
      .then((data) => {
        const generatedQuestions = generateQuestionsFromWiki(data.extract);
        setQuiz(generatedQuestions);
      });
  }, []);

  const generateQuestionsFromWiki = (text) => {
    const sampleQuestions = [
      {
        question: "Messi'nin tam adı nedir?",
        options: [
          "Lionel Andrés Messi Cuccittini",
          "Lionel Alberto Messi",
          "Lionel Javier Messi",
          "Lionel Alejandro Messi"
        ],
        answer: "Lionel Andrés Messi Cuccittini"
      },
      {
        question: "Messi'nin doğum yılı nedir?",
        options: ["1985", "1986", "1987", "1988"],
        answer: "1987"
      }
    ];
    return sampleQuestions.sort(() => 0.5 - Math.random()).slice(0, 10);
  };

  const handleAnswer = (answer) => {
    if (quiz[currentQuestion]?.answer === answer) {
      setScore(score + 1);
    }
    if (currentQuestion + 1 < quiz.length) {
      setCurrentQuestion(currentQuestion + 1);
    } else {
      setGameOver(true);
    }
  };

  return (
    <div className="p-5 flex flex-col items-center">
      {!gameOver ? (
        <Card className="w-96 p-5">
          <CardContent>
            <h2 className="text-xl font-bold mb-4">{quiz[currentQuestion]?.question}</h2>
            {quiz[currentQuestion]?.options.map((option, index) => (
              <Button
                key={index}
                className="w-full my-2"
                onClick={() => handleAnswer(option)}
              >
                {option}
              </Button>
            ))}
          </CardContent>
        </Card>
      ) : (
        <Card className="w-96 p-5 text-center">
          <CardContent>
            <h2 className="text-2xl font-bold mb-4">Quiz Bitti!</h2>
            <p className="text-lg">Skorun: {score} / {quiz.length}</p>
            <Button className="mt-4" onClick={() => window.location.reload()}>
              Yeni Sorularla Oyna
            </Button>
          </CardContent>
        </Card>
      )}
    </div>
  );
}
