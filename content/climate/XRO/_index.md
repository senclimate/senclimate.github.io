---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

linktitle: "ENSO Forecast"
summary: "Climate hindicasts and forecasts using the Extended nonlinear recharge oscillator (XRO) model "
weight: 2

# Page metadata.
title: Operational XRO Climate Forecasts
date: "2024-08-09T00:00:00Z"
lastmod: "2024-08-09T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: book  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.

---

### 📝 XRO Niño3.4 SST anomaly monthly forecast

<style>
  #image-selector {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px;
    background-color: #f1f1f1; /* Light grey background */
    border-radius: 5px; /* Rounded corners */
  }

  #image-selector label, #image-selector select, #image-selector button {
    margin: 0;
    padding: 8px 12px;
    font-size: 16px;
    border: 1px solid #ccc; /* Grey border */
    border-radius: 4px; /* Rounded corners for inputs and buttons */
  }

  button {
    background-color: #007bff; /* Bootstrap primary color */
    color: white;
    cursor: pointer;
    border: none;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #0056b3; /* Darker blue on hover */
  }

  select {
    cursor: pointer;
  }
  #image-display {
    text-align: center; /* Centers the content inside this div */
    padding: 10px; /* Adds some padding around the content */
  }

  #selectedImage {
    width: 99%; /* Sets the image width to 80% of its container */
    max-width: 100%; /* Ensures the image does not exceed the size of the container */
    height: auto; /* Maintains the aspect ratio of the image */
    display: block; /* Makes the image a block element to apply width and centering */
    margin: 0 auto; /* Centers the image horizontally within its container */
  }

  #imageStatus {
    color: red;
    font-size: 16px; /* Sets the font size for the status message */
  }
  .references {
    list-style: none; /* Removes default list styling */
    padding: 0; /* Removes padding */
  }

  .references li {
    margin: 0 0 10px 0; /* Adds space between items */
    padding-left: 2ch; /* Adds padding to create space for hanging indent */
    text-indent: -2ch; /* Creates hanging indent */
  }
</style>


<div id="image-selector">
  <label for="yearDropdown">Select the ENSO Forecast:</label>
  <select id="yearDropdown" onchange="updateImage()"></select>
  <select id="monthDropdown" onchange="updateImage()">
    <option value="01">Jan</option>
    <option value="02">Feb</option>
    <option value="03">Mar</option>
    <option value="04">Apr</option>
    <option value="05">May</option>
    <option value="06">Jun</option>
    <option value="07">Jul</option>
    <option value="08">Aug</option>
    <option value="09">Sep</option>
    <option value="10">Oct</option>
    <option value="11">Nov</option>
    <option value="12">Dec</option>
  </select>
  <button onclick="changeMonth(-1)">Previous Month</button>
  <button onclick="changeMonth(1)">Next Month</button>
</div>

<div id="image-display">
  <img id="selectedImage" src="" alt="Selected Image" style="display: none;">
  <p id="imageStatus" style="display: none;">Image unavailable for the selected date.</p>
</div>

<script>
  function populateYears() {
    const yearDropdown = document.getElementById('yearDropdown');
    const startYear = 2023;
    const endYear = 2028;
    const currentYear = new Date().getFullYear();

    for (let year = startYear; year <= endYear; year++) {
      const option = document.createElement('option');
      option.value = year;
      option.text = year;
      yearDropdown.appendChild(option);
    }

    yearDropdown.value = Math.min(currentYear, endYear); // default to current or max available
  }

  function updateImage() {
    const year = document.getElementById('yearDropdown').value;
    const month = document.getElementById('monthDropdown').value;
    const imagePath = `/XRO_plume/${year}-${month}_Nino34.png`;

    const img = document.getElementById('selectedImage');
    const status = document.getElementById('imageStatus');

    const testImg = new Image();
    testImg.onload = function () {
      img.src = imagePath;
      img.style.display = 'block';
      status.style.display = 'none';
    };
    testImg.onerror = function () {
      img.style.display = 'none';
      status.style.display = 'block';
    };
    testImg.src = imagePath;
  }

  function setDefaultMonth() {
    const monthDropdown = document.getElementById('monthDropdown');
    const today = new Date();
    const day = today.getDate();
    const monthIndex = today.getMonth(); // 0-based

    // Default to previous month if before 15th
    monthDropdown.selectedIndex = (day <= 15) ? (monthIndex + 11) % 12 : monthIndex;
    updateImage();
  }

  function changeMonth(delta) {
    const monthDropdown = document.getElementById('monthDropdown');
    const yearDropdown = document.getElementById('yearDropdown');

    let currentMonthIndex = monthDropdown.selectedIndex;
    let currentYearIndex = yearDropdown.selectedIndex;

    const totalMonths = 12;
    const newMonthIndex = currentMonthIndex + delta;

    // Handle month rollover
    if (newMonthIndex < 0) {
      if (currentYearIndex > 0) {
        yearDropdown.selectedIndex = currentYearIndex - 1;
        monthDropdown.selectedIndex = totalMonths - 1;
      }
    } else if (newMonthIndex >= totalMonths) {
      if (currentYearIndex < yearDropdown.options.length - 1) {
        yearDropdown.selectedIndex = currentYearIndex + 1;
        monthDropdown.selectedIndex = 0;
      }
    } else {
      monthDropdown.selectedIndex = newMonthIndex;
    }

    updateImage();
  }

  window.onload = function () {
    populateYears();
    setDefaultMonth();
  };
</script>



### XRO model 

The XRO is an e**X**tended nonlinear **R**echarge **O**scillator model for El Niño-Southern Oscillation (ENSO) and other modes of variability in the global oceans ([Zhao et al. 2024](#ref-zhao-2024)). It builds on the legacies of the Hasselmann stochastic climate model capturing upper ocean memory in sea surface temperature (SST) variability ([Hasselmann, 1976](#ref-hasselmann-1976)), and the recharge oscillator model for the oscillatory core dynamics of ENSO ([Jin, 1997](#ref-jin-1997)). It constitutes a parsimonious representation of the climate system in a reduced variable and parameter space that still captures the essential dynamics of interconnected global climate variability. For the detailed formulation of XRO model, please refer to our paper ([Zhao et al., 2024](#ref-zhao-2024)).


### XRO ENSO forecast skill
![Forecast correlation skill (ACC) for Niño3.4 across model combinations derived from different SST and WWV data](/XRO_skills/XRO_Nino34_out_of_sample_skill_2012-2024.png)
**Figure 1**: Out-of-sample forecast accuracy from XRO trained on 1982–2011 data and verified over 2012–2024. Lines show correlation skill as a function of lead month for different combinations of SST and WWV datasets (e.g., `OISSTv2_godas`, `ERA5_oras5`, etc.).

![Forecast correlation skill (ACC) for Niño3.4 across model combinations derived from different SST and WWV data](/XRO_skills/XRO_Nino34_in_sample_skill_1982-2024.png)
**Figure 2**: In-sample forecast accuracy from XRO trained on 1982–2024.

### Data source

Operationally, we produce 18-month forecasts using the trained XRO model based on climate mode indices from 1982–2022, with initial conditions starting in January 2023. The XRO state vectors include ENSO and other climate modes, derived from:

- **Monthly SST anomaly indices**, based on:
  - [OISST v2.1](https://psl.noaa.gov/data/gridded/data.noaa.oisst.v2.highres.html) provided by NOAA/PSL
  - [ERA5](https://doi.org/10.24381/cds.f17050d7) provided by the Copernicus Climate Change Service (C3S)
  - [ORAS5](https://doi.org/10.24381/cds.67e8eeb7) SST provided by C3S
  - [GODAS](https://psl.noaa.gov/data/gridded/data.godas.html) SST provided by NOAA/PSL

- **Monthly Warm Water Volume (WWV) index** of equatorial Pacific upper-ocean heat content, based on:
  - [TAO](https://www.pmel.noaa.gov/elnino/upper-ocean-heat-content-and-enso) data provided by NOAA/PMEL
  - [IAPv4 subsurface temperature](http://www.ocean.iap.ac.cn/ftp/cheng/IAPv4.2_IAP_Temperature_gridded_1month_netcdf) provided by Lijing Cheng at IAP, Chinese Academy of Sciences
  - [ORAS5](https://doi.org/10.24381/cds.67e8eeb7) D20 provided by C3S 
  - [GODAS](https://psl.noaa.gov/data/gridded/data.godas.html) provided by NOAA/PSL

We conduct 1000-member stochastic forecasts with the same initial conditions for each month but different stochastic forcings, See Supplementary Fig. 16 in [Zhao et al. (2024)](#ref-zhao-2024) for how we make 1000-member stochastic forecasts in details.

Due to delays in TAO updates, the OISSTv2_IAPv4 version has been adopted for the official release starting June 2025.

### References

<ul class="references">
  <li><a id="ref-zhao-2024"></a>Zhao, S., Jin, F.-F., Stuecker, M. F., Thompson, P. R., Kug, J.-S., McPhaden, M. J., et al. (2024). Explainable El Niño predictability from climate mode interactions. <strong><em>Nature, 630</em></strong>(8018), 891–898. <a href="https://doi.org/10.1038/s41586-024-07534-6">https://doi.org/10.1038/s41586-024-07534-6</a></li>

  <li><a id="ref-jin-1997"></a>Jin, F.-F. (1997). An equatorial ocean recharge paradigm for ENSO. Part I: conceptual model. <strong><em>Journal of the Atmospheric Sciences, 54</em></strong>, 811–829. <a href="https://doi.org/10.1175/1520-0469(1997)054<0811:aeorpf>2.0.co;2">https://doi.org/10.1175/1520-0469(1997)054&lt;0811:aeorpf&gt;2.0.co;2</a></li>

  <li><a id="ref-hasselmann-1976"></a>Hasselmann, K. (1976). Stochastic climate models Part I. Theory. <strong><em>Tellus, 28</em></strong>(6), 473–485. <a href="https://doi.org/10.1111/j.2153-3490.1976.tb00696.x">https://doi.org/10.1111/j.2153-3490.1976.tb00696.x</a></li>
</ul>




{{% callout warning %}}
Disclaimer: 

The XRO forecast is provided for informational and academic research purposes and is not intended for production use. This website and its affiliated entities expressly disclaim any liability for decisions or actions based on the reliance on this information. Furthermore, no responsibility is assumed for any consequential, special, or similar damages resulting from such reliance.
{{% /callout %}}
