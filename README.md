# COMproject final
import React, { useState } from 'react';
import { Plus, Trash2, RotateCw, ChevronLeft, ChevronRight } from 'lucide-react';

export default function FlashcardApp() {
  const [cards, setCards] = useState([
    { id: 1, front: 'What is React?', back: 'A JavaScript library for building user interfaces' },
    { id: 2, front: 'What is JSX?', back: 'A syntax extension for JavaScript that looks similar to HTML' }
  ]);
  const [currentIndex, setCurrentIndex] = useState(0);
  const [isFlipped, setIsFlipped] = useState(false);
  const [isAdding, setIsAdding] = useState(false);
  const [newFront, setNewFront] = useState('');
  const [newBack, setNewBack] = useState('');

  const handleFlip = () => setIsFlipped(!isFlipped);

  const handleNext = () => {
    if (currentIndex < cards.length - 1) {
      setCurrentIndex(currentIndex + 1);
      setIsFlipped(false);
    }
  };

  const handlePrevious = () => {
    if (currentIndex > 0) {
      setCurrentIndex(currentIndex - 1);
      setIsFlipped(false);
    }
  };

  const handleAddCard = () => {
    if (newFront.trim() && newBack.trim()) {
      const newCard = {
        id: Date.now(),
        front: newFront,
        back: newBack
      };
      setCards([...cards, newCard]);
      setNewFront('');
      setNewBack('');
      setIsAdding(false);
    }
  };

  const handleDeleteCard = (id) => {
    const filtered = cards.filter(card => card.id !== id);
    setCards(filtered);
    if (currentIndex >= filtered.length && filtered.length > 0) {
      setCurrentIndex(filtered.length - 1);
    } else if (filtered.length === 0) {
      setCurrentIndex(0);
    }
    setIsFlipped(false);
  };

  const handleShuffle = () => {
    const shuffled = [...cards].sort(() => Math.random() - 0.5);
    setCards(shuffled);
    setCurrentIndex(0);
    setIsFlipped(false);
  };

  return (
    <div className="min-h-screen bg-white">
      <div className="max-w-4xl mx-auto px-4 py-8">
        {/* Header */}
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold text-gray-800 mb-2">Flashcard Study</h1>
          <p className="text-gray-600">Master your learning with interactive flashcards</p>
        </div>

        {/* Stats */}
        <div className="flex justify-center gap-4 mb-8">
          <div className="bg-gray-50 px-6 py-3 rounded-lg border border-gray-200">
