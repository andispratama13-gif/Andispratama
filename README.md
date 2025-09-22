# Andispratama
Lomba cerdas cermat
import { useState } from "react";

export default function App() { // Contoh soal const questions = [ { question: "Sebutkan planet di tata surya!", answers: [ { text: "Merkurius", points: 20 }, { text: "Venus", points: 20 }, { text: "Bumi", points: 20 }, { text: "Mars", points: 20 }, { text: "Jupiter", points: 10 }, { text: "Saturnus", points: 5 }, { text: "Uranus", points: 3 }, { text: "Neptunus", points: 2 }, ], }, { question: "Tokoh proklamasi Indonesia?", answers: [ { text: "Soekarno", points: 50 }, { text: "Moh. Hatta", points: 50 }, ], }, ];

const [qIndex, setQIndex] = useState(0); const [revealed, setRevealed] = useState([]); const [scores, setScores] = useState([0, 0]);

const currentQ = questions[qIndex];

const revealAnswer = (i) => { if (!revealed.includes(i)) { setRevealed([...revealed, i]); } };

const addScore = (team, points) => { const newScores = [...scores]; newScores[team] += points; setScores(newScores); };

const nextQuestion = () => { setQIndex((qIndex + 1) % questions.length); setRevealed([]); };

return ( <div className="min-h-screen bg-blue-900 text-white flex flex-col items-center p-6"> <h1 className="text-3xl font-bold mb-4">🎮 Family 100 SMA Edition</h1>

{/* Papan skor */}
  <div className="flex gap-6 mb-6">
    {scores.map((score, i) => (
      <div key={i} className="bg-yellow-500 text-black p-4 rounded-2xl shadow-xl">
        Tim {i + 1}: {score}
      </div>
    ))}
  </div>

  {/* Soal */}
  <h2 className="text-xl mb-4">❓ {currentQ.question}</h2>

  {/* Jawaban */}
  <div className="grid grid-cols-2 gap-4 w-full max-w-2xl">
    {currentQ.answers.map((ans, i) => (
      <div
        key={i}
        className="bg-gray-800 p-4 rounded-xl flex justify-between items-center cursor-pointer"
        onClick={() => revealAnswer(i)}
      >
        {revealed.includes(i) ? (
          <>
            <span>{ans.text}</span>
            <button
              className="bg-green-500 text-black px-2 py-1 rounded"
              onClick={(e) => {
                e.stopPropagation();
                addScore(0, ans.points); // default untuk Tim 1
              }}
            >+{ans.points}</button>
            <button
              className="bg-red-500 text-black px-2 py-1 rounded"
              onClick={(e) => {
                e.stopPropagation();
                addScore(1, ans.points); // default untuk Tim 2
              }}
            >+{ans.points}</button>
          </>
        ) : (
          <span>────────</span>
        )}
      </div>
    ))}
  </div>

  {/* Tombol kontrol */}
  <div className="mt-6 flex gap-4">
    <button onClick={nextQuestion} className="bg-purple-500 px-4 py-2 rounded-xl">
      Soal Berikutnya
    </button>
  </div>
</div>

); }

