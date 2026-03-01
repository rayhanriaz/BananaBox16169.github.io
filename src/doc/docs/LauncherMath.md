# Dynamic Equations

The program below display the equations we use to calculate our hood angle, flywheel RPM, turret tracking, and velocity corrections in order to maintain a consistent launch throughout the field.

## Turret Tracking

```java
if (result != null && result.isValid()) {
    double txRad = Math.toRadians(result.getTx());

    txRad = ((txRad + Math.PI) % (2 * Math.PI)) - Math.PI;

    // PIDF calculations
    turretIntegral += txRad * dt;
    double derivative = (txRad - lastError) / dt;

    double output =
        turretKp * txRad +
                turretKi * turretIntegral +
                turretKd * derivative +
                turretKf * Math.signum(txRad);

    turret.setPower(output);
    lastError = txRad;
} 
else {
    turret.setPower(0);
}
```
This is the equation we use to track the goal with our turret. We utilize PIDF, standing for Proportional, Integral, Derivative, and Feedforward. P adjusts how aggressively the turret turns to face the goal, and I allows the turret to track
the center of the tag by scaling the power up until reaching the center. D controls the power dampening as the turret approaches the goal, eliminating overshoot. Finally, F controls the minimum required power to move the turret to account 
for friction. 

## Hood Angle
```java
double hoodAngle = A * Math.sqrt(filteredTa) + B;  // hood angle in degrees

hoodAngle = clamp(hoodAngle, 23, 58);

// Convert to servo position
hood.setPosition(angleToServo(hoodAngle));
```

```java
private double angleToServo(double angleDeg){
    // Map hood angle (degrees) to servo position (0-1)
    // 1 = 58° (fully down), 0 = 23° (fully up)
    double servoPos = (58.0 - angleDeg) / (58.0 - 23.0);
    return clamp(servoPos, 0, 1);
}
```
This code shows the equation used to calculate the hood angle, where A is the scale factor, filteredTa is the % of the camera screen the april tag takes up, and B is the starting value of the hood. 
This ensures that the angle of the hood is constantly adjusting based off of the distance from the goal.

## Velocity and Flywheel RPM

```java
double turretAngle =
        turret.getCurrentPosition() * TICKS_TO_RAD;

double vForward =
        velocity.getXComponent() * Math.cos(turretAngle)
                + velocity.getYComponent() * Math.sin(turretAngle);

// flywheel RPM
double targetRPM =
        C * Math.sqrt(filteredTa) + D;

// Backward compensation only
targetRPM += (-vForward) * RPM_PER_MPS;
targetRPM = clamp(targetRPM, MIN_RPM, MAX_RPM);

double TPS = targetRPM * 28 / 60;


            flywheel1.setVelocity(TPS);
            flywheel2.setVelocity(TPS);
}
```

The equation for the flywheel RPM is the same as the hood ange except C replaces A and D replaces B. The velocity compensation is built into the same equation as the flywheel RPM so that the RPM can adjust while on the move. The velocity equation
allows us to shoot while the robot is in motion, which is very versatile, especially for this season, due to the numerous collisions occurring throughout the match. The equation gathers and stores the turret’s current position in radians,
then collects the velocity of the robot and calculates what the angle the turret, flywheel RPM, and hood angle need to be in order to land in the goal.

## Pedro Pathing

We use Pedro Pathing to create our paths in auto and to get the current velocity of the robot which is used by our velocity equation. For the auto paths we use a tool called [Pedro Pathing Visualizer](https://visualizer.pedropathing.com/), this allows us to
draw out our paths instead of guessing the coordinates. Pedro Pathing also has a built-in command to find the current velocity of the robot. Overall Pedro Pathing is one of the best open-source tools out there for FTC.


[Contact us](https://mail.google.com/mail/u/0/?fs=1&to=ftcbananabox16169@gmail.com&tf=cm){ .md-button }

