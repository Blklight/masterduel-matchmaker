<template>
  <filter
    id="blue-black"
    x="-10%"
    y="-10%"
    width="120%"
    height="120%"
    filterUnits="objectBoundingBox"
    primitiveUnits="userSpaceOnUse"
    color-interpolation-filters="sRGB"
  >
    <feColorMatrix
      type="matrix"
      values=".33 .33 .33 0 0
            .33 .33 .33 0 0
            .33 .33 .33 0 0
            0 0 0 1 0"
      in="SourceGraphic"
      result="colormatrix"
    />
    <feComponentTransfer in="colormatrix" result="componentTransfer">
      <feFuncR type="table" tableValues="0.07 0" />
      <feFuncG type="table" tableValues="0.07 0.84" />
      <feFuncB type="table" tableValues="0.07 1" />
      <feFuncA type="table" tableValues="0 1" />
    </feComponentTransfer>
    <feBlend
      mode="normal"
      in="componentTransfer"
      in2="SourceGraphic"
      result="blend"
    />
  </filter>
</template>
