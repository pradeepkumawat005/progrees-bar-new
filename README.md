# progrees-bar-new
<body>
    <div class="container">
        <div class="progress-container">
            <div class="progress" id="progress"></div>
            <div class="text-wrap active">
                <div class="circle">1</div>
                <p class="text">Customer</p>
            </div>
            <div class="text-wrap">
                <div class="circle">2</div>
                <p class="text">Delivery</p>
            </div>
            <div class="text-wrap">
                <div class="circle">3</div>
                <p class="text">Payment</p>
            </div>
            <div class="text-wrap">
                <div class="circle">4</div>
                <p class="text">Review</p>
            </div>
            <div class="text-wrap">
                <div class="circle">5</div>
                <p class="text">Feedback</p>
            </div>
            <div class="text-wrap">
                <div class="circle">6</div>
                <p class="text">Support</p>
            </div>
            <div class="text-wrap">
                <div class="circle">7</div>
                <p class="text">Follow-up</p>
            </div>
        </div>
        <button class="btn" id="back" disabled>&larr; Back</button>
        <button class="btn" id="next">Next &rarr;</button>
    </div>
    <script src="./script.js"></script>
</body>





:root {
    --color:  oklch(86.63% 0.25 148.01);
    --line-border-empty: oklch(76.63% 0.25 148.01);
    --text-empty:        oklch(71.63% 0.25 148.01);
    --line-border-fill:  oklch(64.29% 0.26 360);
    --text-fill:         oklch(46.63% 0.25 148.01);
} 

* {
    box-sizing: border-box;
}

body {
    background-color: var(--color);
    font-family: 'Inter', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
    margin: 0;
}

.container {
    text-align: center;
}

.progress-container {
    display: flex;
    justify-content: space-between;
    position: relative;
    margin-bottom: 30px;
    max-width: 100%;
    width: calc(200px * 7); /* Adjust width to fit all steps */
}

.progress-container::before {
    content: '';
    background-color: var(--line-border-empty);
    position: absolute;
    top: 18px;
    left: 0;
    transform: translateY(-50%);
    height: 4px;
    width: calc(200px * 6); /* Adjust width to fit all steps */
    z-index: -1;
}

.progress {
    background-color: var(--line-border-fill);
    position: absolute;
    top: 18px;
    left: 0;
    transform: translateY(-50%);
    height: 4px;
    width: 0%;
    z-index: -1;
    transition: 400ms ease;
}

.text-wrap {
    display: inline-block;
    text-align: center;
    width: 200px; /* Fixed width for each step */
}

.text-wrap p {
    font-weight: 400;
    font-size: 12px;
    color: var(--text-empty);
}

.text-wrap.active p {
    font-weight: 500;
    color: var(--text-fill);
    transition: 400ms ease;
}

.circle {
    background-color: var(--color);
    border: 3px solid var(--line-border-empty);
    color: var(--text-empty);
    font-weight: 600;
    border-radius: 50%;
    height: 35px;
    width: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: 400ms ease;
}

.text-wrap.active .circle {
    border-color: var(--line-border-fill);
    color: var(--text-fill);
}

.btn {
    background-color: var(--line-border-fill);
    color: white;
    border: 0;
    border-radius: 5px;
    cursor: pointer;
    font-family: inherit;
    padding: 10px 30px;
    margin: 5px;
    font-size: 14px;
}

.btn:active {
    transform: scale(0.98);
}

.btn:focus {
    outline: 0;
}

.btn:disabled {
    background-color: var(--line-border-empty);
    cursor: not-allowed;
    color: var(--color);
    transform: none;
}


const progress = document.getElementById('progress');
const back = document.getElementById('back');
const next = document.getElementById('next');
const wraps = document.querySelectorAll('.text-wrap');

let currentActive = 1; // Start with the first step always active

function update() {
    wraps.forEach((wrap, index) => {
        if (index < currentActive) {
            wrap.classList.add('active');
        } else {
            wrap.classList.remove('active');
        }
    });

    const actives = document.querySelectorAll('.active');
    // Calculate the progress width
    progress.style.width = ((actives.length - 1) / (wraps.length - 1)) * (200 * (wraps.length - 1)) + 'px';

    // Update button states
    back.disabled = currentActive === 1;
    next.disabled = currentActive === wraps.length;
}

// Initialize the progress bar and button states
update();

next.addEventListener('click', () => {
    if (currentActive < wraps.length) {
        currentActive++;
        update();
    }
});

back.addEventListener('click', () => {
    if (currentActive > 1) {
        currentActive--;
        update();
    }
  
  
});   
