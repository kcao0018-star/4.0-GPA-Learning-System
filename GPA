import React, { useState, useEffect } from 'react';
import { CheckCircle, XCircle, AlertCircle, RotateCcw, ChevronRight } from 'lucide-react';

const LearningSystemMatrix = () => {
  const [concepts, setConcepts] = useState([]);
  const [newConcept, setNewConcept] = useState('');
  const [currentView, setCurrentView] = useState('overview');
  const [selectedConcept, setSelectedConcept] = useState(null);

  useEffect(() => {
    const saved = localStorage.getItem('learningConcepts');
    if (saved) {
      setConcepts(JSON.parse(saved));
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('learningConcepts', JSON.stringify(concepts));
  }, [concepts]);

  const addConcept = () => {
    if (newConcept.trim()) {
      const concept = {
        id: Date.now(),
        name: newConcept,
        status: 'not-started',
        steps: {
          acquisition: { complete: false, notes: '' },
          feynman: { complete: false, notes: '' },
          theory: { complete: false, score: 0, total: 5 },
          application: { complete: false, score: 0, total: 5 },
          gateway: { passed: false }
        },
        reviews: [],
        createdAt: new Date().toISOString()
      };
      setConcepts([...concepts, concept]);
      setNewConcept('');
    }
  };

  const updateStep = (conceptId, step, data) => {
    setConcepts(concepts.map(c => {
      if (c.id === conceptId) {
        const updated = { ...c };
        updated.steps[step] = { ...updated.steps[step], ...data };
        
        if (step === 'application' && data.score === 5) {
          updated.steps.gateway.passed = true;
          updated.status = 'mastered';
        }
        
        return updated;
      }
      return c;
    }));
  };

  const addReview = (conceptId) => {
    setConcepts(concepts.map(c => {
      if (c.id === conceptId) {
        return {
          ...c,
          reviews: [...c.reviews, {
            date: new Date().toISOString(),
            score: 0,
            total: 5,
            passed: false
          }]
        };
      }
      return c;
    }));
  };

  const updateReview = (conceptId, reviewIndex, score) => {
    setConcepts(concepts.map(c => {
      if (c.id === conceptId) {
        const reviews = [...c.reviews];
        reviews[reviewIndex] = {
          ...reviews[reviewIndex],
          score: score,
          passed: score === 5
        };
        return { ...c, reviews };
      }
      return c;
    }));
  };

  const resetConcept = (conceptId) => {
    setConcepts(concepts.map(c => {
      if (c.id === conceptId) {
        return {
          ...c,
          status: 'not-started',
          steps: {
            acquisition: { complete: false, notes: '' },
            feynman: { complete: false, notes: '' },
            theory: { complete: false, score: 0, total: 5 },
            application: { complete: false, score: 0, total: 5 },
            gateway: { passed: false }
          }
        };
      }
      return c;
    }));
  };

  const deleteConcept = (conceptId) => {
    setConcepts(concepts.filter(c => c.id !== conceptId));
    if (selectedConcept?.id === conceptId) {
      setSelectedConcept(null);
      setCurrentView('overview');
    }
  };

  const getStatusColor = (status) => {
    switch (status) {
      case 'mastered': return 'bg-green-100 text-green-800';
      case 'in-progress': return 'bg-yellow-100 text-yellow-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  };

  const ConceptCard = ({ concept }) => (
    <div 
      className="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow cursor-pointer border-l-4 border-blue-500"
      onClick={() => {
        setSelectedConcept(concept);
        setCurrentView('detail');
      }}
    >
      <div className="flex justify-between items-start mb-4">
        <h3 className="text-xl font-bold text-gray-800">{concept.name}</h3>
        <span className={`px-3 py-1 rounded-full text-sm font-medium ${getStatusColor(concept.status)}`}>
          {concept.status === 'mastered' ? 'Mastered' : concept.status === 'in-progress' ? 'In Progress' : 'Not Started'}
        </span>
      </div>
      
      <div className="space-y-2">
        <div className="flex items-center gap-2">
          {concept.steps.acquisition.complete ? <CheckCircle className="w-5 h-5 text-green-500" /> : <div className="w-5 h-5 rounded-full border-2 border-gray-300" />}
          <span className="text-sm text-gray-600">Concept Acquisition</span>
        </div>
        <div className="flex items-center gap-2">
          {concept.steps.feynman.complete ? <CheckCircle className="w-5 h-5 text-green-500" /> : <div className="w-5 h-5 rounded-full border-2 border-gray-300" />}
          <span className="text-sm text-gray-600">Feynman Filter</span>
        </div>
        <div className="flex items-center gap-2">
          {concept.steps.theory.complete ? <CheckCircle className="w-5 h-5 text-green-500" /> : <div className="w-5 h-5 rounded-full border-2 border-gray-300" />}
          <span className="text-sm text-gray-600">Theory Questions ({concept.steps.theory.score}/5)</span>
        </div>
        <div className="flex items-center gap-2">
          {concept.steps.gateway.passed ? <CheckCircle className="w-5 h-5 text-green-500" /> : <div className="w-5 h-5 rounded-full border-2 border-gray-300" />}
          <span className="text-sm text-gray-600">Application Gateway ({concept.steps.application.score}/5)</span>
        </div>
      </div>
      
      {concept.reviews.length > 0 && (
        <div className="mt-4 pt-4 border-t border-gray-200">
          <p className="text-sm text-gray-600">24h Reviews: {concept.reviews.filter(r => r.passed).length}/{concept.reviews.length} passed</p>
        </div>
      )}
    </div>
  );

  const ConceptDetail = ({ concept }) => (
    <div className="bg-white rounded-lg shadow-lg p-8">
      <div className="flex justify-between items-start mb-6">
        <div>
          <button 
            onClick={() => setCurrentView('overview')}
            className="text-blue-600 hover:text-blue-800 mb-2 flex items-center gap-1"
          >
            ← Back to Overview
          </button>
          <h2 className="text-3xl font-bold text-gray-800">{concept.name}</h2>
        </div>
        <div className="flex gap-2">
          <button
            onClick={() => resetConcept(concept.id)}
            className="px-4 py-2 bg-yellow-500 text-white rounded-lg hover:bg-yellow-600 flex items-center gap-2"
          >
            <RotateCcw className="w-4 h-4" />
            Reset
          </button>
          <button
            onClick={() => deleteConcept(concept.id)}
            className="px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600"
          >
            Delete
          </button>
        </div>
      </div>

      <div className="space-y-6">
        {/* Step 3.1: Concept Acquisition */}
        <div className="border rounded-lg p-6 bg-gray-50">
          <div className="flex items-center gap-3 mb-4">
            <div className="bg-blue-500 text-white rounded-full w-8 h-8 flex items-center justify-center font-bold">1</div>
            <h3 className="text-xl font-semibold">Concept Acquisition</h3>
          </div>
          <p className="text-gray-600 mb-4">Read or watch source material until the logic is clear.</p>
          <textarea
            className="w-full p-3 border rounded-lg mb-3"
            placeholder="Add notes about your understanding..."
            value={concept.steps.acquisition.notes}
            onChange={(e) => updateStep(concept.id, 'acquisition', { notes: e.target.value })}
            rows="3"
          />
          <button
            onClick={() => updateStep(concept.id, 'acquisition', { complete: !concept.steps.acquisition.complete })}
            className={`px-4 py-2 rounded-lg font-medium ${concept.steps.acquisition.complete ? 'bg-green-500 text-white' : 'bg-gray-300 text-gray-700'}`}
          >
            {concept.steps.acquisition.complete ? 'Completed ✓' : 'Mark Complete'}
          </button>
        </div>

        {/* Step 3.2: Feynman Filter */}
        <div className="border rounded-lg p-6 bg-gray-50">
          <div className="flex items-center gap-3 mb-4">
            <div className="bg-blue-500 text-white rounded-full w-8 h-8 flex items-center justify-center font-bold">2</div>
            <h3 className="text-xl font-semibold">The Feynman Filter</h3>
          </div>
          <p className="text-gray-600 mb-4">Explain in plain English. No jargon. A 10-year-old should understand.</p>
          <textarea
            className="w-full p-3 border rounded-lg mb-3"
            placeholder="Write your explanation here..."
            value={concept.steps.feynman.notes}
            onChange={(e) => updateStep(concept.id, 'feynman', { notes: e.target.value })}
            rows="4"
          />
          <button
            onClick={() => updateStep(concept.id, 'feynman', { complete: !concept.steps.feynman.complete })}
            className={`px-4 py-2 rounded-lg font-medium ${concept.steps.feynman.complete ? 'bg-green-500 text-white' : 'bg-gray-300 text-gray-700'}`}
          >
            {concept.steps.feynman.complete ? 'Completed ✓' : 'Mark Complete'}
          </button>
        </div>

        {/* Step 3.3: Theory Questions */}
        <div className="border rounded-lg p-6 bg-gray-50">
          <div className="flex items-center gap-3 mb-4">
            <div className="bg-blue-500 text-white rounded-full w-8 h-8 flex items-center justify-center font-bold">3</div>
            <h3 className="text-xl font-semibold">Initial Calibration - Theory</h3>
          </div>
          <p className="text-gray-600 mb-4">Attempt 5 practice questions on conceptual theory.</p>
          <div className="flex items-center gap-4 mb-3">
            <label className="text-gray-700 font-medium">Score:</label>
            <input
              type="number"
              min="0"
              max="5"
              value={concept.steps.theory.score}
              onChange={(e) => {
                const score = parseInt(e.target.value) || 0;
                updateStep(concept.id, 'theory', { score: Math.min(5, Math.max(0, score)), complete: score >= 5 });
              }}
              className="w-20 p-2 border rounded-lg"
            />
            <span className="text-gray-600">/ 5</span>
          </div>
          {concept.steps.theory.score === 5 && (
            <div className="flex items-center gap-2 text-green-600 font-medium">
              <CheckCircle className="w-5 h-5" />
              Theory questions complete!
            </div>
          )}
        </div>

        {/* Step 3.4 & 3.5: Application Gateway */}
        <div className="border rounded-lg p-6 bg-gray-50">
          <div className="flex items-center gap-3 mb-4">
            <div className="bg-blue-500 text-white rounded-full w-8 h-8 flex items-center justify-center font-bold">4</div>
            <h3 className="text-xl font-semibold">5/5 Gateway - Application</h3>
          </div>
          <p className="text-gray-600 mb-2">Attempt 5 application-based problem-solving questions.</p>
          <p className="text-red-600 font-semibold mb-4">⚠️ You MUST score 5/5 to proceed to next concept!</p>
          <div className="flex items-center gap-4 mb-3">
            <label className="text-gray-700 font-medium">Score:</label>
            <input
              type="number"
              min="0"
              max="5"
              value={concept.steps.application.score}
              onChange={(e) => {
                const score = parseInt(e.target.value) || 0;
                updateStep(concept.id, 'application', { score: Math.min(5, Math.max(0, score)), complete: score === 5 });
              }}
              className="w-20 p-2 border rounded-lg"
            />
            <span className="text-gray-600">/ 5</span>
          </div>
          {concept.steps.application.score === 5 ? (
            <div className="flex items-center gap-2 text-green-600 font-bold text-lg">
              <CheckCircle className="w-6 h-6" />
              GATEWAY PASSED! Concept Mastered!
            </div>
          ) : concept.steps.application.score > 0 ? (
            <div className="flex items-center gap-2 text-red-600 font-medium">
              <XCircle className="w-5 h-5" />
              Gateway not passed. Return to Step 1 and re-digest material.
            </div>
          ) : null}
        </div>

        {/* 24-Hour Reviews */}
        <div className="border rounded-lg p-6 bg-gray-50">
          <div className="flex items-center justify-between mb-4">
            <h3 className="text-xl font-semibold">24-Hour Reviews</h3>
            <button
              onClick={() => addReview(concept.id)}
              className="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600"
            >
              Add Review
            </button>
          </div>
          {concept.reviews.length === 0 ? (
            <p className="text-gray-500 italic">No reviews yet. Add one after 24 hours.</p>
          ) : (
            <div className="space-y-3">
              {concept.reviews.map((review, idx) => (
                <div key={idx} className="flex items-center gap-4 p-3 bg-white rounded border">
                  <span className="text-gray-600">Review {idx + 1}</span>
                  <input
                    type="number"
                    min="0"
                    max="5"
                    value={review.score}
                    onChange={(e) => updateReview(concept.id, idx, parseInt(e.target.value) || 0)}
                    className="w-20 p-2 border rounded"
                  />
                  <span className="text-gray-600">/ 5</span>
                  {review.passed ? (
                    <span className="text-green-600 font-medium flex items-center gap-1">
                      <CheckCircle className="w-4 h-4" /> Passed
                    </span>
                  ) : review.score > 0 ? (
                    <span className="text-red-600 font-medium flex items-center gap-1">
                      <XCircle className="w-4 h-4" /> Failed - Review again
                    </span>
                  ) : null}
                </div>
              ))}
            </div>
          )}
        </div>
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 p-8">
      <div className="max-w-7xl mx-auto">
        <header className="mb-8">
          <h1 className="text-4xl font-bold text-gray-800 mb-2">4.0 GPA Learning System</h1>
          <p className="text-gray-600">Target: 90-100% Achievement on All Assessments</p>
        </header>

        {currentView === 'overview' ? (
          <>
            <div className="bg-white rounded-lg shadow-md p-6 mb-8">
              <h2 className="text-2xl font-bold mb-4">Add New Concept</h2>
              <div className="flex gap-3">
                <input
                  type="text"
                  value={newConcept}
                  onChange={(e) => setNewConcept(e.target.value)}
                  onKeyPress={(e) => e.key === 'Enter' && addConcept()}
                  placeholder="Enter concept name (e.g., Quadratic Equations)"
                  className="flex-1 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                />
                <button
                  onClick={addConcept}
                  className="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 font-medium flex items-center gap-2"
                >
                  Add Concept <ChevronRight className="w-5 h-5" />
                </button>
              </div>
            </div>

            <div className="mb-6">
              <h2 className="text-2xl font-bold mb-4">Your Concepts</h2>
              <div className="flex gap-4 mb-4">
                <span className="text-gray-600">Total: {concepts.length}</span>
                <span className="text-green-600">Mastered: {concepts.filter(c => c.status === 'mastered').length}</span>
                <span className="text-yellow-600">In Progress: {concepts.filter(c => c.status === 'in-progress').length}</span>
              </div>
            </div>

            {concepts.length === 0 ? (
              <div className="bg-white rounded-lg shadow-md p-12 text-center">
                <AlertCircle className="w-16 h-16 text-gray-400 mx-auto mb-4" />
                <h3 className="text-xl font-semibold text-gray-600 mb-2">No concepts yet</h3>
                <p className="text-gray-500">Add your first concept to start your journey to mastery!</p>
              </div>
            ) : (
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                {concepts.map(concept => (
                  <ConceptCard key={concept.id} concept={concept} />
                ))}
              </div>
            )}
          </>
        ) : (
          <ConceptDetail concept={selectedConcept} />
        )}
      </div>
    </div>
  );
};

export default LearningSystemMatrix;
