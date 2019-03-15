<template>
  <svg
    width="104px"
    height="104px"
    viewBox="0 0 104 104"
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
  >
    <defs>
      <circle id="path-1" cx="36" cy="36" r="36"></circle>
      <filter
        x="-37.5%"
        y="-29.2%"
        width="175.0%"
        height="175.0%"
        filterUnits="objectBoundingBox"
        id="filter-2"
      >
        <feOffset
          dx="0"
          dy="6"
          in="SourceAlpha"
          result="shadowOffsetOuter1"
        ></feOffset>
        <feGaussianBlur
          stdDeviation="8"
          in="shadowOffsetOuter1"
          result="shadowBlurOuter1"
        ></feGaussianBlur>
        <feColorMatrix
          values="0 0 0 0 0.0117647059   0 0 0 0 0.0862745098   0 0 0 0 0.160784314  0 0 0 0.08 0"
          type="matrix"
          in="shadowBlurOuter1"
          result="shadowMatrixOuter1"
        ></feColorMatrix>
        <feOffset
          dx="0"
          dy="1"
          in="SourceAlpha"
          result="shadowOffsetOuter2"
        ></feOffset>
        <feGaussianBlur
          stdDeviation="1"
          in="shadowOffsetOuter2"
          result="shadowBlurOuter2"
        ></feGaussianBlur>
        <feColorMatrix
          values="0 0 0 0 0.0117647059   0 0 0 0 0.0862745098   0 0 0 0 0.160784314  0 0 0 0.11 0"
          type="matrix"
          in="shadowBlurOuter2"
          result="shadowMatrixOuter2"
        ></feColorMatrix>
        <feMerge>
          <feMergeNode in="shadowMatrixOuter1"></feMergeNode>
          <feMergeNode in="shadowMatrixOuter2"></feMergeNode>
        </feMerge>
      </filter>
    </defs>
    <g
      id="Page-1"
      stroke="none"
      stroke-width="1"
      fill="none"
      fill-rule="evenodd"
    >
      <g id="Artboard" transform="translate(-460.000000, -125.000000)">
        <g id="Group-4" transform="translate(412.000000, 129.000000)">
          <g id="Drive-icon-" transform="translate(58.000000, 0.000000)">
            <circle
              id="Oval"
              fill="#2196F3"
              opacity="0.100000001"
              cx="42"
              cy="42"
              r="42"
            ></circle>
            <g id="Group" transform="translate(6.000000, 6.000000)">
              <g id="Oval">
                <use
                  fill="black"
                  fill-opacity="1"
                  filter="url(#filter-2)"
                  xlink:href="#path-1"
                ></use>
                <use
                  fill="#FFFFFF"
                  fill-rule="evenodd"
                  xlink:href="#path-1"
                ></use>
              </g>
              <g
                id="google-drive"
                transform="translate(20.000000, 22.000000)"
                fill-rule="nonzero"
              >
                <polygon
                  id="Path"
                  fill="#FFC107"
                  points="21.4163769 20.1846154 32 20.1846154 21.4163769 0 10.8307692 0"
                ></polygon>
                <polygon
                  id="Path"
                  fill="#2196F3"
                  points="9.97143698 20.1846154 5.41538462 28.0615385 27.01526 28.0615385 32 20.1846154"
                ></polygon>
                <polygon
                  id="Path"
                  fill="#4CAF50"
                  points="10.6240847 0 0 18.7070242 5.3130384 28.0615385 15.7538462 9.67722198"
                ></polygon>
              </g>
            </g>
          </g>
        </g>
      </g>
    </g></svg
></template>
<script>
export default {
  name: "UploadIcon"
};
</script>
