# Geometric_Color_Radiant
let dim;
let angleSpeed = 0.005; // Setting a smaller value for slower rotation

function setup() {
  createCanvas(640, 360);
  dim = width; // Set to width for large shape
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();
  frameRate(10); // Lower frame rate for slower animation
}

let angle = 0;

function draw() {
  background(220, 50, 50); // Medium blue in HSB
  angle += angleSpeed; // Increment angle
  
  drawComplexGradient(width / 2, height / 2, angle);
}

function drawComplexGradient(x, y, angle) {
  let maxRadius = dim / 2;
  let h = random(0, 360);
  let step = 20;

  for (let r = maxRadius; r > 0; r -= step) {
    let lerpFactor = map(r, 0, maxRadius, 0, 1);
    let newHue = lerp(h, (h + 180) % 360, lerpFactor);
    fill(newHue, 90, 90, (1 - lerpFactor) * 100);

    // Draw Ellipse
    ellipse(x, y, r * 2, r * 2);

    // Draw Square
    push();
    translate(x, y);
    rotate(angle); // Use the incrementing angle here
    rect(-r, -r, r * 2, r * 2);
    pop();

    // Draw Triangle
    push();
    translate(x, y);
    rotate(-angle); // Use the opposite of the incrementing angle here
    triangle(-r, -r, r, -r, 0, r);
    pop();
  }
}
