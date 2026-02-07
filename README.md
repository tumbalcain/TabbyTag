
<a id="readme-top"></a>

<!-- PROJECT SHIELDS -->
<!--
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![project_license][license-shield]][license-url]



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/tumbalcain/TabbyTag">
    <img src="images/TabbyTag Logo White.png" alt="Logo" height="80" width="auto">
    <hr>
  </a>

  ### Built With [![Java][Java]][Java-url]
 
  <p align="center">
    Beginner-friendly AprilTag Pipeline for FTC
    <br />
    <a href="https://github.com/tumbalcain/TabbyTag"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/tumbalcain/TabbyTag">View Demo</a>
    &middot;
    <a href="https://github.com/tumbalcain/TabbyTag/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/tumbalcain/TabbyTag/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

**TabbyTag** is a beginner-friendly AprilTag pipeline designed for easy comprehension and implementation. It offers straightforward functionality suitable for a range of applications. The pipeline was developed by Axander, a programmer from the FTC team R2045.

TabbyTag handles:
- AprilTag detection
- Tag ID parsing
- Pose estimation (if enabled)

This allows teams to focus on robot logic instead of vision math.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

This is the instruction on how to use TabbyTag in your FTC robot code (autonomous/teleop). This instruction will get the TabbyTag pipeline run with minimal setup and readable code.

### Prerequisites

Before using TabbyTag, make sure you have:

- An FTC Robot Controller project (Android Studio recommended)
- A compatible webcam supported by the FTC SDK
- FTC SDK version 8.2 or newer
- Basic familiarity with Java (classes, functions, variables)

### Installation

1. Clone the repository
    ```sh
        git clone clone https://github.com/tumbalcain/TabbyTag.git
    ```
2. Copy the TabbyTag source files into your FTC project
    ```
    TeamCode
    ├── java
    │  └── org.firstinspires.ftc.teamcode
    │     └── TabbyTag.java <--
    └── manifests
    ```
3. Sync and build the project to ensure there are no errors
4. Plug in your webcam and verify it is detected by the FTC Robot Controller

**Optional extra:**
> If you’re using OnBot Java, manually paste the source files instead of cloning.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

1. Create a TabbyTag pipeline instance
2. Attach it to your camera
3. Read detected AprilTag data during autonomous or teleop

**Example Usage**

```
TabbyTag tabbyTag = new TabbyTag()

private final CRServo turret;
static final double KP = 0.1;
static final double DEADBAND = 1.5;

public void init() {
    tabbyTag.init(hardwareMap, telemetry);
    turret = hardwareMap.get(CRServo.class, "turret");
}

public void loop() {
    tabbyTag.update();

    double bearing = tabbyTag.getBearingToTag(24);

    if (Math.abs(bearing) < DEADBAND) {
        turret.setPower(0);
        return true;
    } // end of conditional

    double power = Math.max(-0.3, Math.min(0.3, bearing * KP));
    turret.setPower(power);
}

public void stop() {
    tabbyTag.stop()
}
```

### **⚠️ ATTENTION ⚠️**

Most the of TabbyTag functions return `-1` if there are no AprilTags detected. For example:

```
public double getDistanceToTag(int id) {
        AprilTagDetection tag = getTagBySpecificId(id);
        return (tag != null) ? tag.ftcPose.z : -1;
}
```

And also, please insert `tabbyTag.update();` inside the `loop()` function.

<!-- _For more examples, please refer to the [Documentation](https://example.com)_ -->

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

Planned improvements for TabbyTag include:

- [ ] Cleaner API for accessing detection data
- [ ] Multiple-tag detection support
- [ ] Better documentation and diagrams
- [ ] Performance optimizations for low-end devices
- [ ] Example autonomous routines using AprilTags

See the [open issues](https://github.com/tumbalcain/TabbyTag/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are welcome, especially from FTC students and mentors.

If you want to help improve TabbyTag:
- Improve documentation or comments
- Add example OpModes
- Optimize performance
- Fix bugs or edge cases

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Top contributors:

<a href="https://github.com/tumbalcain/TabbyTag/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=tumbalcain/TabbyTag" alt="contrib.rocks image" />
</a>



<!-- LICENSE -->
## License

Distributed under the project_license. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

A. Sinsustra - [arslan.sinsustra@gmail.com](arslan.sinsustra@gmail.com)

Project Link: [https://github.com/tumbalcain/TabbyTag](https://github.com/tumbalcain/TabbyTag)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

Special thanks to:

- FIRST Tech Challenge community and documentation
- The creators of AprilTag and OpenCV
- FTC teams who experiment, break things, and share fixes
- Open-source contributors whose work made this pipeline possible

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/tumbalcain/TabbyTag.svg?style=for-the-badge
[contributors-url]: https://github.com/tumbalcain/TabbyTag/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/tumbalcain/TabbyTag.svg?style=for-the-badge
[forks-url]: https://github.com/tumbalcain/TabbyTag/network/members
[stars-shield]: https://img.shields.io/github/stars/tumbalcain/TabbyTag.svg?style=for-the-badge
[stars-url]: https://github.com/tumbalcain/TabbyTag/stargazers
[issues-shield]: https://img.shields.io/github/issues/tumbalcain/TabbyTag.svg?style=for-the-badge
[issues-url]: https://github.com/tumbalcain/TabbyTag/issues
[license-shield]: https://img.shields.io/github/license/tumbalcain/TabbyTag.svg?style=for-the-badge
[license-url]: https://github.com/tumbalcain/TabbyTag/blob/master/LICENSE.txt
[product-screenshot]: images/screenshot.png
<!-- Shields.io badges. You can a comprehensive list with many more badges at: https://github.com/inttter/md-badges -->
[Java]: https://img.shields.io/badge/Java-%23ED8B00.svg?logo=openjdk&logoColor=white
[Java-url]: https://ftc-docs.firstinspires.org/en/latest/programming_resources/onbot_java/OnBot-Java-Tutorial.html