<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>4.0 GPA Learning System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(to bottom right, #eff6ff, #e0e7ff);
            min-height: 100vh;
            padding: 2rem;
        }
        
        .container {
            max-width: 1280px;
            margin: 0 auto;
        }
        
        header {
            margin-bottom: 2rem;
        }
        
        h1 {
            font-size: 2.25rem;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 0.5rem;
        }
        
        .subtitle {
            color: #4b5563;
        }
        
        .card {
            background: white;
            border-radius: 0.5rem;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
            padding: 1.5rem;
            margin-bottom: 2rem;
        }
        
        .input-group {
            display: flex;
            gap: 0.75rem;
        }
        
        input[type="text"], textarea {
            flex: 1;
            padding: 0.75rem;
            border: 1px solid #d1d5db;
            border-radius: 0.5rem;
            font-size: 1rem;
            font-family: inherit;
        }
        
        input[type="number"] {
            width: 5rem;
            padding: 0.5rem;
            border: 1px solid #d1d5db;
            border-radius: 0.5rem;
        }
        
        button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 0.5rem;
            cursor: pointer;
            font-weight: 500;
            font-size: 1rem;
        }
        
        .btn-primary {
            background: #2563eb;
            color: white;
        }
        
        .btn-primary:hover {
            background: #1d4ed8;
        }
        
        .btn-success {
            background: #10b981;
            color: white;
        }
        
        .btn-warning {
            background: #eab308;
            color: white;
        }
        
        .btn-danger {
            background: #ef4444;
            color: white;
        }
        
        .btn-secondary {
            background: #d1d5db;
            color: #374151;
        }
        
        .concepts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 1.5rem;
        }
        
        .concept-card {
            background: white;
            border-radius: 0.5rem;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
            padding: 1.5rem;
            cursor: pointer;
            border-left: 4px solid #3b82f6;
            transition: box-shadow 0.3s;
        }
        
        .concept-card:hover {
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
        }
        
        .concept-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 1rem;
        }
        
        .status-badge {
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        .status-mastered {
            background: #d1fae5;
            color: #065f46;
        }
        
        .status-progress {
            background: #fef3c7;
            color: #92400e;
        }
        
        .status-not-started {
            background: #f3f4f6;
            color: #1f2937;
        }
        
        .step-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.5rem;
            font-size: 0.875rem;
            color: #4b5563;
        }
        
        .checkbox {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            border: 2px solid #d1d5db;
            display: inline-block;
        }
        
        .checkbox.checked {
            background: #10b981;
            border-color: #10b981;
            position: relative;
        }
        
        .checkbox.checked::after {
            content: '✓';
            color: white;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 14px;
        }
        
        .step-section {
            border: 1px solid #e5e7eb;
            border-radius: 0.5rem;
            padding: 1.5rem;
            background: #f9fafb;
            margin-bottom: 1.5rem;
        }
        
        .step-header {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            margin-bottom: 1rem;
        }
        
        .step-number {
            background: #3b82f6;
            color: white;
            border-radius: 50%;
            width: 2rem;
            height: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        .alert-success {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: #059669;
            font-weight: 500;
            margin-top: 0.5rem;
        }
        
        .alert-error {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: #dc2626;
            font-weight: 500;
            margin-top: 0.5rem;
        }
        
        .alert-warning {
            color: #dc2626;
            font-weight: 600;
            margin-bottom: 1rem;
        }
        
        .hidden {
            display: none;
        }
        
        .back-link {
            color: #2563eb;
            background: none;
            border: none;
            cursor: pointer;
            margin-bottom: 0.5rem;
            font-size: 1rem;
            padding: 0;
        }
        
        .back-link:hover {
            color: #1d4ed8;
        }
        
        .button-group {
            display: flex;
            gap: 0.5rem;
        }
        
        .stats {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
        }
        
        .review-item {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 0.75rem;
            background: white;
            border-radius: 0.25rem;
            border: 1px solid #e5e7eb;
            margin-bottom: 0.75rem;
        }
        
        .empty-state {
            text-align: center;
            padding: 3rem;
            color: #6b7280;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>4.0 GPA Learning System</h1>
            <p class="subtitle">Target: 90-100% Achievement on All Assessments</p>
        </header>

        <div id="overviewView">
            <div class="card">
                <h2 style="font-size: 1.5rem; font-weight: bold; margin-bottom: 1rem;">Add New Concept</h2>
                <div class="input-group">
                    <input type="text" id="newConceptInput" placeholder="Enter concept name (e.g., Quadratic Equations)">
                    <button class="btn-primary" onclick="addConcept()">Add Concept →</button>
                </div>
            </div>

            <div style="margin-bottom: 1.5rem;">
                <h2 style="font-size: 1.5rem; font-weight: bold; margin-bottom: 1rem;">Your Concepts</h2>
                <div class="stats">
                    <span style="color: #4b5563;">Total: <span id="totalCount">0</span></span>
                    <span style="color: #059669;">Mastered: <span id="masteredCount">0</span></span>
                    <span style="color: #d97706;">In Progress: <span id="progressCount">0</span></span>
                </div>
            </div>

            <div id="conceptsList" class="concepts-grid"></div>
            <div id="emptyState" class="card empty-state hidden">
                <p style="font-size: 1.25rem; font-weight: 600; color: #4b5563; margin-bottom: 0.5rem;">No concepts yet</p>
                <p>Add your first concept to start your journey to mastery!</p>
            </div>
        </div>

        <div id="detailView" class="hidden">
            <div class="card" style="padding: 2rem;">
                <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 1.5rem;">
                    <div>
                        <button class="back-link" onclick="showOverview()">← Back to Overview</button>
                        <h2 id="detailTitle" style="font-size: 1.875rem; font-weight: bold; color: #1f2937;"></h2>
                    </div>
                    <div class="button-group">
                        <button class="btn-warning" onclick="resetConcept()">Reset</button>
                        <button class="btn-danger" onclick="deleteConcept()">Delete</button>
                    </div>
                </div>

                <div id="detailSteps"></div>
            </div>
        </div>
    </div>

    <script>
        let concepts = [];
        let currentConceptId = null;

        // Load concepts from localStorage
        function loadConcepts() {
            const saved = localStorage.getItem('learningConcepts');
            if (saved) {
                concepts = JSON.parse(saved);
            }
            renderOverview();
        }

        // Save concepts to localStorage
        function saveConcepts() {
            localStorage.setItem('learningConcepts', JSON.stringify(concepts));
        }

        // Add new concept
        function addConcept() {
            const input = document.getElementById('newConceptInput');
            const name = input.value.trim();
            
            if (name) {
                const concept = {
                    id: Date.now(),
                    name: name,
                    status: 'not-started',
                    steps: {
                        acquisition: { complete: false, notes: '' },
                        feynman: { complete: false, notes: '' },
                        theory: { complete: false, score: 0 },
                        application: { complete: false, score: 0 },
                        gateway: { passed: false }
                    },
                    reviews: []
                };
                
                concepts.push(concept);
                saveConcepts();
                input.value = '';
                renderOverview();
            }
        }

        // Render overview
        function renderOverview() {
            const list = document.getElementById('conceptsList');
            const empty = document.getElementById('emptyState');
            
            document.getElementById('totalCount').textContent = concepts.length;
            document.getElementById('masteredCount').textContent = concepts.filter(c => c.status === 'mastered').length;
            document.getElementById('progressCount').textContent = concepts.filter(c => c.status === 'in-progress').length;
            
            if (concepts.length === 0) {
                list.innerHTML = '';
                empty.classList.remove('hidden');
            } else {
                empty.classList.add('hidden');
                list.innerHTML = concepts.map(concept => `
                    <div class="concept-card" onclick="showDetail(${concept.id})">
                        <div class="concept-header">
                            <h3 style="font-size: 1.25rem; font-weight: bold; color: #1f2937;">${concept.name}</h3>
                            <span class="status-badge status-${concept.status === 'mastered' ? 'mastered' : concept.status === 'in-progress' ? 'progress' : 'not-started'}">
                                ${concept.status === 'mastered' ? 'Mastered' : concept.status === 'in-progress' ? 'In Progress' : 'Not Started'}
                            </span>
                        </div>
                        <div>
                            <div class="step-item">
                                <span class="checkbox ${concept.steps.acquisition.complete ? 'checked' : ''}"></span>
                                <span>Concept Acquisition</span>
                            </div>
                            <div class="step-item">
                                <span class="checkbox ${concept.steps.feynman.complete ? 'checked' : ''}"></span>
                                <span>Feynman Filter</span>
                            </div>
                            <div class="step-item">
                                <span class="checkbox ${concept.steps.theory.complete ? 'checked' : ''}"></span>
                                <span>Theory Questions (${concept.steps.theory.score}/5)</span>
                            </div>
                            <div class="step-item">
                                <span class="checkbox ${concept.steps.gateway.passed ? 'checked' : ''}"></span>
                                <span>Application Gateway (${concept.steps.application.score}/5)</span>
                            </div>
                        </div>
                        ${concept.reviews.length > 0 ? `
                            <div style="margin-top: 1rem; padding-top: 1rem; border-top: 1px solid #e5e7eb;">
                                <p style="font-size: 0.875rem; color: #4b5563;">
                                    24h Reviews: ${concept.reviews.filter(r => r.passed).length}/${concept.reviews.length} passed
                                </p>
                            </div>
                        ` : ''}
                    </div>
                `).join('');
            }
        }

        // Show detail view
        function showDetail(id) {
            currentConceptId = id;
            const concept = concepts.find(c => c.id === id);
            
            document.getElementById('overviewView').classList.add('hidden');
            document.getElementById('detailView').classList.remove('hidden');
            document.getElementById('detailTitle').textContent = concept.name;
            
            renderDetail(concept);
        }

        // Render detail view
        function renderDetail(concept) {
            const stepsHtml = `
                <div class="step-section">
                    <div class="step-header">
                        <div class="step-number">1</div>
                        <h3 style="font-size: 1.25rem; font-weight: 600;">Concept Acquisition</h3>
                    </div>
                    <p style="color: #4b5563; margin-bottom: 1rem;">Read or watch source material until the logic is clear.</p>
                    <textarea id="acquisitionNotes" rows="3" style="width: 100%; margin-bottom: 0.75rem;" placeholder="Add notes about your understanding...">${concept.steps.acquisition.notes}</textarea>
                    <button class="btn-${concept.steps.acquisition.complete ? 'success' : 'secondary'}" onclick="toggleStep('acquisition')">
                        ${concept.steps.acquisition.complete ? 'Completed ✓' : 'Mark Complete'}
                    </button>
                </div>

                <div class="step-section">
                    <div class="step-header">
                        <div class="step-number">2</div>
                        <h3 style="font-size: 1.25rem; font-weight: 600;">The Feynman Filter</h3>
                    </div>
                    <p style="color: #4b5563; margin-bottom: 1rem;">Explain in plain English. No jargon. A 10-year-old should understand.</p>
                    <textarea id="feynmanNotes" rows="4" style="width: 100%; margin-bottom: 0.75rem;" placeholder="Write your explanation here...">${concept.steps.feynman.notes}</textarea>
                    <button class="btn-${concept.steps.feynman.complete ? 'success' : 'secondary'}" onclick="toggleStep('feynman')">
                        ${concept.steps.feynman.complete ? 'Completed ✓' : 'Mark Complete'}
                    </button>
                </div>

                <div class="step-section">
                    <div class="step-header">
                        <div class="step-number">3</div>
                        <h3 style="font-size: 1.25rem; font-weight: 600;">Initial Calibration - Theory</h3>
                    </div>
                    <p style="color: #4b5563; margin-bottom: 1rem;">Attempt 5 practice questions on conceptual theory.</p>
                    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 0.75rem;">
                        <label style="color: #374151; font-weight: 500;">Score:</label>
                        <input type="number" id="theoryScore" min="0" max="5" value="${concept.steps.theory.score}" onchange="updateScore('theory', this.value)">
                        <span style="color: #4b5563;">/ 5</span>
                    </div>
                    ${concept.steps.theory.score === 5 ? '<div class="alert-success">✓ Theory questions complete!</div>' : ''}
                </div>

                <div class="step-section">
                    <div class="step-header">
                        <div class="step-number">4</div>
                        <h3 style="font-size: 1.25rem; font-weight: 600;">5/5 Gateway - Application</h3>
                    </div>
                    <p style="color: #4b5563; margin-bottom: 0.5rem;">Attempt 5 application-based problem-solving questions.</p>
                    <p class="alert-warning">⚠️ You MUST score 5/5 to proceed to next concept!</p>
                    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 0.75rem;">
                        <label style="color: #374151; font-weight: 500;">Score:</label>
                        <input type="number" id="applicationScore" min="0" max="5" value="${concept.steps.application.score}" onchange="updateScore('application', this.value)">
                        <span style="color: #4b5563;">/ 5</span>
                    </div>
                    ${concept.steps.application.score === 5 ? 
                        '<div class="alert-success" style="font-size: 1.125rem; font-weight: bold;">✓ GATEWAY PASSED! Concept Mastered!</div>' :
                        concept.steps.application.score > 0 ?
                        '<div class="alert-error">✗ Gateway not passed. Return to Step 1 and re-digest material.</div>' : ''
                    }
                </div>

                <div class="step-section">
                    <div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 1rem;">
                        <h3 style="font-size: 1.25rem; font-weight: 600;">24-Hour Reviews</h3>
                        <button class="btn-primary" onclick="addReview()">Add Review</button>
                    </div>
                    ${concept.reviews.length === 0 ? 
                        '<p style="color: #6b7280; font-style: italic;">No reviews yet. Add one after 24 hours.</p>' :
                        concept.reviews.map((review, idx) => `
                            <div class="review-item">
                                <span style="color: #4b5563;">Review ${idx + 1}</span>
                                <input type="number" min="0" max="5" value="${review.score}" onchange="updateReview(${idx}, this.value)">
                                <span style="color: #4b5563;">/ 5</span>
                                ${review.passed ? '<span class="alert-success">✓ Passed</span>' : 
                                  review.score > 0 ? '<span class="alert-error">✗ Failed - Review again</span>' : ''}
                            </div>
                        `).join('')
                    }
                </div>
            `;
            
            document.getElementById('detailSteps').innerHTML = stepsHtml;
        }

        // Toggle step completion
        function toggleStep(step) {
            const concept = concepts.find(c => c.id === currentConceptId);
            concept.steps[step].complete = !concept.steps[step].complete;
            
            if (step === 'acquisition') {
                concept.steps.acquisition.notes = document.getElementById('acquisitionNotes').value;
            } else if (step === 'feynman') {
                concept.steps.feynman.notes = document.getElementById('feynmanNotes').value;
            }
            
            saveConcepts();
            renderDetail(concept);
        }

        // Update score
        function updateScore(step, value) {
            const concept = concepts.find(c => c.id === currentConceptId);
            const score = Math.min(5, Math.max(0, parseInt(value) || 0));
            
            concept.steps[step].score = score;
            concept.steps[step].complete = score === 5;
            
            if (step === 'application' && score === 5) {
                concept.steps.gateway.passed = true;
                concept.status = 'mastered';
            } else if (step === 'application' && score < 5) {
                concept.steps.gateway.passed = false;
                concept.status = 'in-progress';
            }
            
            saveConcepts();
            renderDetail(concept);
        }

        // Add review
        function addReview() {
            const concept = concepts.find(c => c.id === currentConceptId);
            concept.reviews.push({
                date: new Date().toISOString(),
                score: 0,
                passed: false
            });
            saveConcepts();
            renderDetail(concept);
        }

        // Update review
        function updateReview(idx, value) {
            const concept = concepts.find(c => c.id === currentConceptId);
            const score = Math.min(5, Math.max(0, parseInt(value) || 0));
            
            concept.reviews[idx].score = score;
            concept.reviews[idx].passed = score === 5;
            
            saveConcepts();
            renderDetail(concept);
        }

        // Reset concept
        function resetConcept() {
            if (confirm('Are you sure you want to reset this concept?')) {
                const concept = concepts.find(c => c.id === currentConceptId);
                concept.status = 'not-started';
                concept.steps = {
                    acquisition: { complete: false, notes: '' },
                    feynman: { complete: false, notes: '' },
                    theory: { complete: false, score: 0 },
                    application: { complete: false, score: 0 },
                    gateway: { passed: false }
                };
                saveConcepts();
                renderDetail(concept);
            }
        }

        // Delete concept
        function deleteConcept() {
            if (confirm('Are you sure you want to delete this concept?')) {
                concepts = concepts.filter(c => c.id !== currentConceptId);
                saveConcepts();
                showOverview();
            }
        }

        // Show overview
        function showOverview() {
            document.getElementById('overviewView').classList.remove('hidden');
            document.getElementById('detailView').classList.add('hidden');
            currentConceptId = null;
            renderOverview();
        }

        // Enter key to add concept
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('newConceptInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    addConcept();
                }
            });
            loadConcepts();
        });
    </script>
</body>
</html>
