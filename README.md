# EMitters-lab
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = p5.Vector.random2D();
    this.acceleration = p5.Vector.random2D();
    this.r = 10;
    this.lifespan = 255;
  }

  update() {
    // Apply a soft wind to the right
    let wind = createVector(0.05, 0); // tweak this for stronger wind
    this.applyForce(wind);

    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2;
  }

  isDead() {
    return this.lifespan < 0;
  }

  draw() {
    // Warm orange fading out
    fill(255, 140, 0, this.lifespan);
    noStroke();
    circle(this.position.x, this.position.y, this.r);
  }

  applyForce(f) {
    this.acceleration.add(f);
  }

  static createStandardParticleAt(x, y) {
    return new Particle(x, y);
  }
}
