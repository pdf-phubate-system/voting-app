import { useState, useRef } from "react";
import { motion, AnimatePresence, Reorder } from "framer-motion";
import {
  Plus, Trash2, Image, Type, Vote, ChevronRight,
  RotateCcw, CheckCircle2, Users, Grip, X, BarChart3, ArrowLeft
} from "lucide-react";

const CARD_COLORS = [
  "from-rose-400 to-pink-500",
  "from-violet-400 to-purple-500",
  "from-blue-400 to-cyan-500",
  "from-emerald-400 to-teal-500",
  "from-amber-400 to-orange-500",
  "from-fuchsia-400 to-pink-500",
  "from-sky-400 to-blue-500",
  "from-lime-400 to-green-500",
];

function generateId() {
  return Math.random().toString(36).substr(2, 9);
}

export default function VotingApp() {
  const [mode, setMode] = useState("creator"); // creator | vote | results
  const [questions, setQuestions] = useState([
    { id: generateId(), text: "ทีมที่คุณชอบที่สุด", type: "text" },
  ]);
  const [options, setOptions] = useState([
    { id: generateId(), label: "ตัวเลือก A", type: "text", colorIdx: 0 },
    { id: generateId(), label: "ตัวเลือก B", type: "text", colorIdx: 1 },
    { id: generateId(), label: "ตัวเลือก C", type: "text", colorIdx: 2 },
  ]);
  const [votes, setVotes] = useState({}); // questionId -> optionId[]
  const [draggedOption, setDraggedOption] = useState(null);
  const [overZone, setOverZone] = useState(null);

  // Creator state
  const [newQuestion, setNewQuestion] = useState("");
  const [newOptionLabel, setNewOptionLabel] = useState("");
  const [newOptionType, setNewOptionType] = useState("text");
  const [newOptionValue, setNewOptionValue] = useState("");

  const addQuestion = () => {
    if (!newQuestion.trim()) return;
    setQuestions(prev => [...prev, { id: generateId(), text: newQuestion.trim(), type: "text" }]);
    setNewQuestion("");
  };

  const removeQuestion = (id) => {
    setQuestions(prev => prev.filter(q => q.id !== id));
    setVotes(prev => { const n = { ...prev }; delete n[id]; return n; });
  };

  const addOption = () => {
    if (!newOptionLabel.trim()) return;
    const colorIdx = options.length % CARD_COLORS.length;
    setOptions(prev => [...prev, {
      id: generateId(),
      label: newOptionLabel.trim(),
      type: newOptionType,
      value: newOptionValue.trim() || null,
      colorIdx,
    }]);
    setNewOptionLabel("");
    setNewOptionValue("");
  };

  const removeOption = (id) => {
    setOptions(prev => prev.filter(o => o.id !== id));
    setVotes(prev => {
      const n = {};
      for (const [k, v] of Object.entries(prev)) {
        n[k] = v.filter(oid => oid !== id);
      }
      return n;
    });
  };

  const startVoting = () => {
    setVotes({});
    setMode("vote");
  };

  // Drag handlers
  const handleDragStart = (option) => setDraggedOption(option);
  const handleDragEnd = () => { setDraggedOption(null); setOverZone(null); };

  const handleDropOnZone = (questionId) => {
    if (!draggedOption) return;
    setVotes(prev => {
      const existing = prev[questionId] || [];
      if (existing.includes(draggedOption.id)) return prev;
      return { ...prev, [questionId]: [...existing, draggedOption.id] };
    });
    setDraggedOption(null);
    setOverZone(null);
  };

  const removeVote = (questionId, optionId) => {
    setVotes(prev => ({
      ...prev,
      [questionId]: (prev[questionId] || []).filter(id => id !== optionId),
    }));
  };

  const getOption = (id) => options.find(o => o.id === id);

  const getResults = () => {
    return questions.map(q => {
      const qVotes = votes[q.id] || [];
      const counts = {};
      qVotes.forEach(id => { counts[id] = (counts[id] || 0) + 1; });
      const sorted = Object.entries(counts)
        .map(([id, count]) => ({ option: getOption(id), count }))
        .filter(x => x.option)
        .sort((a, b) => b.count - a.count);
      return { question: q, results: sorted, total: qVotes.length };
    });
  };

  return (
    <div className="min-h-screen bg-[#0f0f13] text-white font-sans" style={{ fontFamily: "'Outfit', sans-serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap');
        .card-drag { cursor: grab; user-select: none; }
        .card-drag:active { cursor: grabbing; }
        .drop-zone-active { border-color: #a78bfa !important; background: rgba(167,139,250,0.08) !important; }
        ::-webkit-scrollbar { width: 4px; } 
        ::-webkit-scrollbar-track { background: #1a1a24; }
        ::-webkit-scrollbar-thumb { background: #3d3d5c; border-radius: 4px; }
      `}</style>

      {/* Header */}
      <header className="border-b border-white/5 bg-[#0f0f13]/80 backdrop-blur-sm sticky top-0 z-50">
        <div className="max-w-6xl mx-auto px-4 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="w-8 h-8 rounded-lg bg-gradient-to-br from-violet-500 to-fuchsia-500 flex items-center justify-center">
              <Vote size={16} />
            </div>
            <span className="font-bold text-lg tracking-tight">VoteDrop</span>
          </div>
          <div className="flex items-center gap-2 bg-white/5 rounded-xl p-1">
            {["creator", "vote", "results"].map(m => (
              <button
                key={m}
                onClick={() => m === "creator" ? setMode("creator") : m === "results" ? setMode("results") : startVoting()}
                className={`px-4 py-1.5 rounded-lg text-sm font-medium transition-all ${
                  mode === m ? "bg-violet-600 text-white shadow-lg shadow-violet-900/50" : "text-white/50 hover:text-white"
                }`}
              >
                {m === "creator" ? "สร้าง" : m === "vote" ? "โหวต" : "ผลลัพธ์"}
              </button>
            ))}
          </div>
        </div>
      </header>

      <div className="max-w-6xl mx-auto px-4 py-8">

        {/* ===== CREATOR MODE ===== */}
        <AnimatePresence mode="wait">
          {mode === "creator" && (
            <motion.div key="creator" initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -20 }}>
              <div className="mb-8">
                <h1 className="text-3xl font-extrabold bg-gradient-to-r from-violet-400 to-fuchsia-400 bg-clip-text text-transparent">โหมดสร้างแบบสอบถาม</h1>
                <p className="text-white/40 mt-1 text-sm">เพิ่มคำถามและตัวเลือกสำหรับการโหวต</p>
              </div>

              <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
                {/* Questions */}
                <div>
                  <h2 className="text-sm font-semibold text-white/60 uppercase tracking-widest mb-4">คำถาม</h2>
                  <div className="space-y-3 mb-4">
                    <AnimatePresence>
                      {questions.map((q, i) => (
                        <motion.div
                          key={q.id}
                          initial={{ opacity: 0, x: -20 }}
                          animate={{ opacity: 1, x: 0 }}
                          exit={{ opacity: 0, x: 20, height: 0 }}
                          className="flex items-center gap-3 bg-white/5 rounded-xl px-4 py-3 group border border-white/5 hover:border-violet-500/30 transition-all"
                        >
                          <span className="text-xs text-white/30 w-5 text-center font-mono">{i + 1}</span>
                          <span className="flex-1 text-sm text-white/80">{q.text}</span>
                          <button onClick={() => removeQuestion(q.id)} className="opacity-0 group-hover:opacity-100 text-red-400 hover:text-red-300 transition-all">
                            <Trash2 size={14} />
                          </button>
                        </motion.div>
                      ))}
                    </AnimatePresence>
                  </div>
                  <div className="flex gap-2">
                    <input
                      value={newQuestion}
                      onChange={e => setNewQuestion(e.target.value)}
                      onKeyDown={e => e.key === "Enter" && addQuestion()}
                      placeholder="พิมพ์คำถาม..."
                      className="flex-1 bg-white/5 border border-white/10 rounded-xl px-4 py-2.5 text-sm outline-none focus:border-violet-500/60 placeholder-white/20 transition-all"
                    />
                    <button onClick={addQuestion} className="bg-violet-600 hover:bg-violet-500 px-4 py-2.5 rounded-xl transition-colors flex items-center gap-1.5 text-sm font-medium">
                      <Plus size={16} /> เพิ่ม
                    </button>
                  </div>
                </div>

                {/* Options */}
                <div>
                  <h2 className="text-sm font-semibold text-white/60 uppercase tracking-widest mb-4">ตัวเลือก (การ์ด)</h2>
                  <div className="grid grid-cols-2 gap-3 mb-4">
                    <AnimatePresence>
                      {options.map(opt => (
                        <motion.div
                          key={opt.id}
                          initial={{ opacity: 0, scale: 0.9 }}
                          animate={{ opacity: 1, scale: 1 }}
                          exit={{ opacity: 0, scale: 0.8 }}
                          className={`relative rounded-xl overflow-hidden group cursor-default`}
                        >
                          <div className={`bg-gradient-to-br ${CARD_COLORS[opt.colorIdx]} p-0.5 rounded-xl`}>
                            <div className="bg-[#1a1a24] rounded-[10px] p-3">
                              {opt.type === "image" && opt.value ? (
                                <img src={opt.value} alt={opt.label} className="w-full h-16 object-cover rounded-lg mb-2" />
                              ) : (
                                <div className={`w-full h-16 rounded-lg mb-2 bg-gradient-to-br ${CARD_COLORS[opt.colorIdx]} opacity-20`} />
                              )}
                              <p className="text-xs font-semibold text-white/80 truncate">{opt.label}</p>
                            </div>
                          </div>
                          <button
                            onClick={() => removeOption(opt.id)}
                            className="absolute top-2 right-2 opacity-0 group-hover:opacity-100 bg-black/60 rounded-full p-1 text-red-400 transition-all"
                          >
                            <X size={10} />
                          </button>
                        </motion.div>
                      ))}
                    </AnimatePresence>
                  </div>

                  {/* Add option form */}
                  <div className="bg-white/3 border border-white/8 rounded-xl p-4 space-y-3">
                    <div className="flex gap-2">
                      <button
                        onClick={() => setNewOptionType("text")}
                        className={`flex-1 flex items-center justify-center gap-2 py-2 rounded-lg text-xs font-medium transition-all ${newOptionType === "text" ? "bg-violet-600 text-white" : "bg-white/5 text-white/40 hover:text-white"}`}
                      >
                        <Type size={12} /> ข้อความ
                      </button>
                      <button
                        onClick={() => setNewOptionType("image")}
                        className={`flex-1 flex items-center justify-center gap-2 py-2 rounded-lg text-xs font-medium transition-all ${newOptionType === "image" ? "bg-violet-600 text-white" : "bg-white/5 text-white/40 hover:text-white"}`}
                      >
                        <Image size={12} /> รูปภาพ
                      </button>
                    </div>
                    <input
                      value={newOptionLabel}
                      onChange={e => setNewOptionLabel(e.target.value)}
                      placeholder="ชื่อตัวเลือก..."
                      className="w-full bg-white/5 border border-white/10 rounded-xl px-3 py-2 text-sm outline-none focus:border-violet-500/60 placeholder-white/20"
                    />
                    {newOptionType === "image" && (
                      <input
                        value={newOptionValue}
                        onChange={e => setNewOptionValue(e.target.value)}
                        placeholder="URL รูปภาพ..."
                        className="w-full bg-white/5 border border-white/10 rounded-xl px-3 py-2 text-sm outline-none focus:border-violet-500/60 placeholder-white/20"
                      />
                    )}
                    <button onClick={addOption} className="w-full bg-violet-600 hover:bg-violet-500 py-2 rounded-xl text-sm font-medium transition-colors flex items-center justify-center gap-2">
                      <Plus size={14} /> เพิ่มตัวเลือก
                    </button>
                  </div>
                </div>
              </div>

              {/* Start Voting Button */}
              {questions.length > 0 && options.length > 0 && (
                <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="mt-10 flex justify-center">
                  <button
                    onClick={startVoting}
                    className="group bg-gradient-to-r from-violet-600 to-fuchsia-600 hover:from-violet-500 hover:to-fuchsia-500 px-8 py-4 rounded-2xl font-bold text-lg flex items-center gap-3 shadow-2xl shadow-violet-900/50 transition-all hover:scale-105 active:scale-95"
                  >
                    <Vote size={22} />
                    เริ่มโหวตได้เลย
                    <ChevronRight size={20} className="group-hover:translate-x-1 transition-transform" />
                  </button>
                </motion.div>
              )}
            </motion.div>
          )}

          {/* ===== VOTE MODE ===== */}
          {mode === "vote" && (
            <motion.div key="vote" initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -20 }}>
              <div className="mb-8 flex items-start justify-between">
                <div>
                  <h1 className="text-3xl font-extrabold bg-gradient-to-r from-cyan-400 to-blue-400 bg-clip-text text-transparent">โหมดโหวต</h1>
                  <p className="text-white/40 mt-1 text-sm">ลากการ์ดไปวางในกล่องคำถามที่ต้องการ</p>
                </div>
                <button onClick={() => setMode("creator")} className="flex items-center gap-2 text-sm text-white/40 hover:text-white transition-colors">
                  <ArrowLeft size={16} /> กลับ
                </button>
              </div>

              {/* Draggable Cards */}
              <div className="mb-8">
                <h2 className="text-xs font-semibold text-white/40 uppercase tracking-widest mb-4 flex items-center gap-2">
                  <Grip size={12} /> ลากการ์ดเหล่านี้
                </h2>
                <div className="flex flex-wrap gap-3">
                  {options.map(opt => (
                    <motion.div
                      key={opt.id}
                      drag
                      dragSnapToOrigin
                      onDragStart={() => handleDragStart(opt)}
                      onDragEnd={handleDragEnd}
                      whileDrag={{ scale: 1.1, zIndex: 100, boxShadow: "0 20px 60px rgba(139,92,246,0.4)" }}
                      whileHover={{ scale: 1.03 }}
                      className="card-drag relative"
                    >
                      <div className={`bg-gradient-to-br ${CARD_COLORS[opt.colorIdx]} p-0.5 rounded-2xl shadow-lg`}>
                        <div className="bg-[#1a1a24] rounded-[14px] p-3 w-36">
                          {opt.type === "image" && opt.value ? (
                            <img src={opt.value} alt={opt.label} className="w-full h-20 object-cover rounded-xl mb-2" onError={e => e.target.style.display = 'none'} />
                          ) : (
                            <div className={`w-full h-20 rounded-xl mb-2 bg-gradient-to-br ${CARD_COLORS[opt.colorIdx]} opacity-30 flex items-center justify-center`}>
                              <Type size={24} className="text-white/40" />
                            </div>
                          )}
                          <p className="text-xs font-semibold text-white text-center truncate">{opt.label}</p>
                        </div>
                      </div>
                    </motion.div>
                  ))}
                </div>
              </div>

              {/* Drop Zones */}
              <div className="space-y-4">
                {questions.map((q, i) => {
                  const qVotes = votes[q.id] || [];
                  const isOver = overZone === q.id;
                  return (
                    <motion.div
                      key={q.id}
                      initial={{ opacity: 0, y: 20 }}
                      animate={{ opacity: 1, y: 0 }}
                      transition={{ delay: i * 0.1 }}
                      onDragOver={e => { e.preventDefault(); setOverZone(q.id); }}
                      onDragLeave={() => setOverZone(null)}
                      onDrop={() => handleDropOnZone(q.id)}
                      className={`border-2 rounded-2xl p-5 transition-all duration-300 ${
                        isOver
                          ? "border-violet-500 bg-violet-500/10"
                          : "border-white/10 bg-white/3 hover:border-white/20"
                      }`}
                    >
                      <div className="flex items-center justify-between mb-4">
                        <div className="flex items-center gap-3">
                          <span className="w-7 h-7 rounded-lg bg-violet-600/30 text-violet-400 text-xs font-bold flex items-center justify-center">{i + 1}</span>
                          <h3 className="font-semibold text-white/90">{q.text}</h3>
                        </div>
                        <span className="text-xs text-white/30 bg-white/5 px-2.5 py-1 rounded-full">
                          {qVotes.length} โหวต
                        </span>
                      </div>

                      {/* Dropped cards */}
                      {qVotes.length === 0 ? (
                        <div className={`border-2 border-dashed rounded-xl p-6 text-center transition-all ${isOver ? "border-violet-500/50" : "border-white/10"}`}>
                          <p className="text-sm text-white/20">วางการ์ดที่นี่</p>
                        </div>
                      ) : (
                        <div className="flex flex-wrap gap-2">
                          <AnimatePresence>
                            {qVotes.map(optId => {
                              const opt = getOption(optId);
                              if (!opt) return null;
                              return (
                                <motion.div
                                  key={`${q.id}-${optId}`}
                                  initial={{ scale: 0, opacity: 0 }}
                                  animate={{ scale: 1, opacity: 1 }}
                                  exit={{ scale: 0, opacity: 0 }}
                                  className="relative group"
                                >
                                  <div className={`bg-gradient-to-br ${CARD_COLORS[opt.colorIdx]} p-0.5 rounded-xl`}>
                                    <div className="bg-[#1a1a24] rounded-[10px] px-3 py-2 flex items-center gap-2">
                                      {opt.type === "image" && opt.value && (
                                        <img src={opt.value} alt="" className="w-6 h-6 rounded object-cover" />
                                      )}
                                      <span className="text-xs font-medium text-white/80">{opt.label}</span>
                                    </div>
                                  </div>
                                  <button
                                    onClick={() => removeVote(q.id, optId)}
                                    className="absolute -top-1.5 -right-1.5 opacity-0 group-hover:opacity-100 bg-red-500 rounded-full p-0.5 transition-all"
                                  >
                                    <X size={8} />
                                  </button>
                                </motion.div>
                              );
                            })}
                          </AnimatePresence>
                        </div>
                      )}
                    </motion.div>
                  );
                })}
              </div>

              <div className="mt-8 flex justify-center">
                <button
                  onClick={() => setMode("results")}
                  className="group bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 px-8 py-4 rounded-2xl font-bold text-lg flex items-center gap-3 shadow-2xl shadow-emerald-900/50 transition-all hover:scale-105 active:scale-95"
                >
                  <BarChart3 size={22} />
                  ดูผลลัพธ์
                  <ChevronRight size={20} className="group-hover:translate-x-1 transition-transform" />
                </button>
              </div>
            </motion.div>
          )}

          {/* ===== RESULTS MODE ===== */}
          {mode === "results" && (
            <motion.div key="results" initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -20 }}>
              <div className="mb-8 flex items-start justify-between">
                <div>
                  <h1 className="text-3xl font-extrabold bg-gradient-to-r from-emerald-400 to-teal-400 bg-clip-text text-transparent">ผลการโหวต</h1>
                  <p className="text-white/40 mt-1 text-sm">สรุปคะแนนทั้งหมด</p>
                </div>
                <div className="flex gap-2">
                  <button onClick={() => setMode("vote")} className="flex items-center gap-2 text-sm text-white/40 hover:text-white bg-white/5 px-3 py-2 rounded-xl transition-all">
                    <RotateCcw size={14} /> โหวตใหม่
                  </button>
                </div>
              </div>

              <div className="space-y-6">
                {getResults().map(({ question, results, total }, i) => (
                  <motion.div
                    key={question.id}
                    initial={{ opacity: 0, y: 20 }}
                    animate={{ opacity: 1, y: 0 }}
                    transition={{ delay: i * 0.1 }}
                    className="bg-white/3 border border-white/8 rounded-2xl p-6"
                  >
                    <div className="flex items-center justify-between mb-5">
                      <div className="flex items-center gap-3">
                        <span className="w-7 h-7 rounded-lg bg-emerald-600/30 text-emerald-400 text-xs font-bold flex items-center justify-center">{i + 1}</span>
                        <h3 className="font-bold text-white">{question.text}</h3>
                      </div>
                      <div className="flex items-center gap-1.5 text-xs text-white/40">
                        <Users size={12} />
                        {total} โหวต
                      </div>
                    </div>

                    {results.length === 0 ? (
                      <p className="text-center text-sm text-white/20 py-4">ยังไม่มีการโหวต</p>
                    ) : (
                      <div className="space-y-3">
                        {results.map(({ option, count }, j) => {
                          const pct = total > 0 ? Math.round((count / total) * 100) : 0;
                          const isWinner = j === 0;
                          return (
                            <div key={option.id} className="group">
                              <div className="flex items-center justify-between mb-1.5">
                                <div className="flex items-center gap-2">
                                  {isWinner && <CheckCircle2 size={14} className="text-emerald-400" />}
                                  {option.type === "image" && option.value && (
                                    <img src={option.value} alt="" className="w-6 h-6 rounded object-cover" />
                                  )}
                                  <span className={`text-sm font-medium ${isWinner ? "text-white" : "text-white/60"}`}>{option.label}</span>
                                </div>
                                <span className={`text-sm font-bold ${isWinner ? "text-emerald-400" : "text-white/40"}`}>{pct}%</span>
                              </div>
                              <div className="h-2 bg-white/5 rounded-full overflow-hidden">
                                <motion.div
                                  initial={{ width: 0 }}
                                  animate={{ width: `${pct}%` }}
                                  transition={{ duration: 0.8, delay: i * 0.1 + j * 0.05, ease: "easeOut" }}
                                  className={`h-full rounded-full bg-gradient-to-r ${CARD_COLORS[option.colorIdx]}`}
                                />
                              </div>
                              <p className="text-xs text-white/20 mt-1">{count} โหวต</p>
                            </div>
                          );
                        })}
                      </div>
                    )}
                  </motion.div>
                ))}
              </div>
            </motion.div>
          )}
        </AnimatePresence>
      </div>
    </div>
  );
}
