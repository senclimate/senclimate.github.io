---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

linktitle: "Climate Monitoring and Forecasts"
summary: ""
weight: 1

# Page metadata.
title: Climate Monitoring and Forecasts
date: "2019-04-09T00:00:00Z"
lastmod: "2019-09-09T00:00:00Z"
draft: true  # Is this a draft? true/false
toc: false  # Show table of contents? true/false
type: book  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
  forecast:
    name: forecast
    weight: 1
---

This page provide 

{{% callout warning %}}
Disclaimer: 
{{% /callout %}}


<style>
  #image-selector {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  #image-selector label, #image-selector select {
    margin: 0;
    font-size: 16px;
  }
</style>

<div id="image-selector">
  <button onclick="changeMonth(-1)">Previous Month</button>

  <label for="yearDropdown">Select a year:</label>
  <select id="yearDropdown" onchange="updateImage()"></select>

  <label for="monthDropdown">Select a month:</label>
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
  <button onclick="changeMonth(1)">Next Month</button>
</div>

<div id="image-display">
  <img id="selectedImage" src="" alt="Selected Image" style="max-width: 100%; display: none;">
  <p id="imageStatus" style="display: none; color: red;">Image unavailable for the selected date.</p>
</div>

<script>
  function populateYears() {
    const yearDropdown = document.getElementById('yearDropdown');
    const currentYear = new Date().getFullYear();
    for (let year = 1982; year <= 2024; year++) {
      let option = document.createElement('option');
      option.value = year;
      option.text = year;
      option.selected = (year === currentYear);
      yearDropdown.appendChild(option);
    }
  }

  function updateImage() {
    var yearDropdown = document.getElementById('yearDropdown');
    var monthDropdown = document.getElementById('monthDropdown');
    var selectedYear = yearDropdown.value;
    var selectedMonth = monthDropdown.value;
    var imagePath = '/XRO_plume/' + selectedYear + '-' + selectedMonth + '.png';

    var img = document.getElementById('selectedImage');
    var status = document.getElementById('imageStatus');

    var testImg = new Image();
    testImg.onload = function() {
      img.src = imagePath;
      img.style.display = 'block';
      status.style.display = 'none';
    };
    testImg.onerror = function() {
      img.style.display = 'none';
      status.style.display = 'block';
    };

    testImg.src = imagePath;
  }

  function setDefaultMonth() {
    const monthDropdown = document.getElementById('monthDropdown');
    const currentDate = new Date();
    const currentDay = currentDate.getDate();
    const currentMonth = currentDate.getMonth(); // JavaScript months are 0-indexed

    if (currentDay <= 9) {
      // If it's on or before the 15th, set the dropdown to the previous month
      monthDropdown.selectedIndex = currentMonth === 0 ? 11 : currentMonth - 1;
    } else {
      // If it's after the 15th, set the dropdown to the current month
      monthDropdown.selectedIndex = currentMonth;
    }

    updateImage();
  }

  function changeMonth(delta) {
    const monthDropdown = document.getElementById('monthDropdown');
    const yearDropdown = document.getElementById('yearDropdown');
    let monthIndex = monthDropdown.selectedIndex + delta;

    if (monthIndex < 0) { // If before January, wrap around to December
      monthIndex = 11;
      changeYear(-1);
    } else if (monthIndex > 11) { // If after December, wrap around to January
      monthIndex = 0;
      changeYear(1);
    }

    monthDropdown.selectedIndex = monthIndex;
    updateImage();
  }

  function changeYear(delta) {
    const yearDropdown = document.getElementById('yearDropdown');
    let yearIndex = yearDropdown.selectedIndex + delta;

    if (yearIndex >= 0 && yearIndex < yearDropdown.options.length) {
      yearDropdown.selectedIndex = yearIndex;
      updateImage();
    }
  }

  window.onload = function() {
    populateYears();
    setDefaultMonth();
  };
</script>


https://iri.columbia.edu/our-expertise/climate/forecasts/enso/current/?enso_tab=enso-sst_table


## [IRI ENSO](https://iri.columbia.edu/our-expertise/climate/forecasts/enso/current/)

* **IRI most recent SST anomaly**
{{< figure src="https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/figure01.gif" title="" numbered="false" lightbox="true" >}}

* **IRI most recent Nino 3.4 SST anomaly index plume**
{{< figure src="https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/figure06.gif" title="" numbered="false" lightbox="true" >}}
https://iri.columbia.edu/our-expertise/climate/forecasts/enso/current/?enso_tab=enso-sst_table

## [JMA ENSO Monitoring and Outlook](https://ds.data.jma.go.jp/tcc/tcc/products/elnino/elmonout.html)

{{< figure src="https://ds.data.jma.go.jp/tcc/tcc/products/elnino/gif/c_sst.gif" title="Monthly mean SST and anomalies in the Pacific and Indian Oceans" numbered="false" lightbox="true" >}}

{{< figure src="https://ds.data.jma.go.jp/tcc/tcc/products/elnino/gif/c_odas.gif" title="Depth-longitude cross sections of temperature and anomalies along the equator in the Indian and Pacific Oceans by the ocean data assimilation system" numbered="false" lightbox="true" >}}

{{< figure src="https://ds.data.jma.go.jp/tcc/tcc/products/elnino/gif/c_eqssta.gif" title="Time-longitude cross section of SST anomalies along the equator in the Indian and Pacific Oceans" numbered="false" lightbox="true" >}}

{{< figure src="https://ds.data.jma.go.jp/tcc/tcc/products/elnino/gif/c_eqohca.gif" title="Time-longitude cross section of ocean heat content (OHC; vertically averaged temperature in the top 300 m) anomalies along the equator in the Indian and Pacific Oceans by the ocean data assimilation system" numbered="false" lightbox="true" >}}

{{< figure src="https://ds.data.jma.go.jp/tcc/tcc/products/elnino/gif/c_olr.gif" title="Monthly mean outgoing longwave radiation (OLR) and anomalies" numbered="false" lightbox="true" >}}


