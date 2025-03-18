import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

export default function GabyLoveSite() {
  const [showMessage, setShowMessage] = useState(false);
  const [quizAnswer, setQuizAnswer] = useState("");
  const [quizResult, setQuizResult] = useState(null);
  const [quizStep, setQuizStep] = useState(0);
  const [message, setMessage] = useState("");

  // Função para quiz com várias perguntas
  const handleQuiz = () => {
    if (quizStep === 0) {
      if (quizAnswer.toLowerCase() === "azul") {
        setQuizResult("Acertou! 💖");
      } else {
        setQuizResult("Errou 😢 Mas te amo mesmo assim!");
      }
      setQuizStep(1);
      setQuizAnswer(""); // Limpa a resposta
    } else if (quizStep === 1) {
      if (quizAnswer.toLowerCase() === "sza") {
        setQuizResult("Acertou! Você conhece muito bem meus gostos musicais! 🎶");
      } else {
        setQuizResult("Errou! Mas a intenção foi boa. 😅");
      }
      setQuizStep(2);
      setQuizAnswer(""); // Limpa a resposta
    } else {
      setQuizResult("Você completou o quiz! 🏆");
    }
  };

  // Função para alterar a mensagem
  const handleChangeMessage = (newMessage) => {
    setMessage(newMessage);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-pink-200 p-4">
      <motion.h1
        className="text-3xl font-bold text-pink-600"
        animate={{ scale: [1, 1.1, 1] }}
        transition={{ duration: 1, repeat: Infinity }}
      >
        💕 Para Meu Momoh 💕
      </motion.h1>

      <Card className="w-80 text-center mt-6 p-4 bg-white shadow-lg rounded-2xl">
        <CardContent>
          <h2 className="text-xl font-semibold text-pink-500">💌 Mensagem Secreta</h2>
          <Button className="mt-3" onClick={() => setShowMessage(!showMessage)}>
            {showMessage ? "Esconder" : "Ver Mensagem"}
          </Button>
          {showMessage && (
            <motion.p
              className="mt-4 text-pink-700"
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
            >
              Moh , você é a cacheadinha mais linda e perfeita do mundo!! ❤️
            </motion.p>
          )}
        </CardContent>
      </Card>

      <Card className="w-80 text-center mt-6 p-4 bg-white shadow-lg rounded-2xl">
        <CardContent>
          <h2 className="text-xl font-semibold text-pink-500">🎮 Quiz: O quanto você me conhece?</h2>
          <p className="text-gray-600">Qual é a minha cor favorita?</p>
          <input
            type="text"
            className="border p-2 mt-2 rounded w-full"
            placeholder="Digite sua resposta..."
            value={quizAnswer}
            onChange={(e) => setQuizAnswer(e.target.value)}
          />
          <Button className="mt-3" onClick={handleQuiz}>Responder</Button>
          {quizResult && <motion.p className="mt-4 font-semibold text-pink-600">{quizResult}</motion.p>}
        </CardContent>
      </Card>

      {/* Se o quiz avançar para a próxima pergunta */}
      {quizStep === 1 && (
        <Card className="w-80 text-center mt-6 p-4 bg-white shadow-lg rounded-2xl">
          <CardContent>
            <h2 className="text-xl font-semibold text-pink-500">🎶 Quiz: Minha música favorita?</h2>
            <p className="text-gray-600">Qual o nome da cantora da música "Saturn"?</p>
            <input
              type="text"
              className="border p-2 mt-2 rounded w-full"
              placeholder="Digite sua resposta..."
              value={quizAnswer}
              onChange={(e) => setQuizAnswer(e.target.value)}
            />
            <Button className="mt-3" onClick={handleQuiz}>Responder</Button>
            {quizResult && <motion.p className="mt-4 font-semibold text-pink-600">{quizResult}</motion.p>}
          </CardContent>
        </Card>
      )}

      {/* Se o quiz for completado */}
      {quizStep === 2 && (
        <motion.div
          className="mt-6 text-center"
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ duration: 1 }}
        >
          <h3 className="text-xl font-semibold text-pink-500">Parabéns, você completou o quiz!</h3>
        </motion.div>
      )}

      {/* Seção de mensagem personalizada */}
      <Card className="w-80 text-center mt-6 p-4 bg-white shadow-lg rounded-2xl">
        <CardContent>
          <h2 className="text-xl font-semibold text-pink-500">💬 Deixe uma mensagem para mim</h2>
          <textarea
            className="border p-2 mt-2 rounded w-full"
            rows="4"
            placeholder="Escreva sua mensagem..."
            value={message}
            onChange={(e) => setMessage(e.target.value)}
          ></textarea>
          <Button className="mt-3" onClick={() => handleChangeMessage(message)}>
            Enviar Mensagem
          </Button>
          {message && (
            <motion.p
              className="mt-4 text-pink-700"
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
            >
              Sua mensagem: {message}
            </motion.p>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
