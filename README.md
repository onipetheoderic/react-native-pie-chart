# react-native-pie-chart

[![npm version](https://img.shields.io/npm/v/react-native-pie-chart)](https://www.npmjs.com/package/react-native-pie-chart)
[![npm downloads](https://img.shields.io/npm/dt/react-native-pie-chart?logo=npm)](https://www.npmjs.com/package/react-native-pie-chart)
[![license](https://img.shields.io/npm/l/react-native-pie-chart)](https://github.com/aidin36/react-native-pie-chart/blob/master/LICENSE)

Simple pie chart module for your React Native app, for both iOS and Android.

<img src="https://raw.githubusercontent.com/aidin36/react-native-pie-chart/main/preview.png" width="400" />

## Installation

You need to have `react`, `react-native` and `react-native-svg` as your app's dependencies.

`react-native-svg` can be installed both in `expo` and in an ejected app. If you had trouble installing `react-native-svg`, refer to the project's documentation: https://www.npmjs.com/package/react-native-svg

Then install this package with:

```bash
npm install github:onipetheoderic/react-native-pie-chart --save
# or
yarn add onipetheoderic/react-native-pie-chart
```

If you're upgrading from an old version, see the upgrade guide below.

## Usage

Here's a quick start code. Refer to the `example` directory for a fully working app.

```tsx
import React, { Component } from 'react'
import { StyleSheet, ScrollView, Text, View } from 'react-native'
import PieChart from 'react-native-pie-chart'

export default class TestChart extends Component {
  render() {
    const widthAndHeight = 250

    const series = [
      { value: 430, color: '#fbd203' },
      { value: 321, color: '#ffb300' },
      { value: 185, color: '#ff9100' },
      { value: 123, color: '#ff6c00' },
    ]

    return (
      <ScrollView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Basic</Text>
          <PieChart widthAndHeight={widthAndHeight} series={series} />

          <Text style={styles.title}>Doughnut</Text>
          <PieChart widthAndHeight={widthAndHeight} series={series} cover={0.45} />
        </View>
      </ScrollView>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
  },
  title: {
    fontSize: 24,
    margin: 10,
  },
})
```

### Adding labels to the chart

For each element in the `series` list, you can also pass a `label` object. It allows you to adjust the font and position of each label. By default, the labels will appear at the center of each slice of the pie. You can use `offsetX` and `offsetY` to move the label.

### 🆕 Multiline label support with `description`

You can now render a two-line label with different styles for each line. Just provide `description` and its style props.

```tsx
const series = [
  {
    value: 40,
    color: '#1E88E5',
    label: {
      text: 'Hallways',
      description: '40%',
      fontSize: 10,
      fontFamily: 'Outfit-Bold',
      descriptionFontSize: 12,
      descriptionFontFamily: 'Outfit-Regular',
      descriptionFill: '#000',
    },
  },
  // more slices...
]
```

This will render:
```
Hallways
   40%
```

## Props

```ts
export type SliceLabel = {
  text: string
  fill?: string
  stroke?: string
  fontSize?: NumberProp
  fontWeight?: FontWeight
  fontFamily?: string
  fontStyle?: FontStyle
  offsetX?: number
  offsetY?: number

  // New optional description line
  description?: string
  descriptionFontSize?: NumberProp
  descriptionFontWeight?: FontWeight
  descriptionFontFamily?: string
  descriptionFontStyle?: FontStyle
  descriptionFill?: string
}

export type Slice = {
  value: number
  color: string
  label?: SliceLabel
}

export type Cover = {
  radius: number
  color?: string
}

export type Props = {
  widthAndHeight: number
  series: Slice[]
  cover?: number | Cover
  style?: StyleProp<ViewStyle>
  padAngle?: number
}
```

## Example App

Have a look at the app in the `example` directory for a complete Typescript app that shows a few charts.
To setup and run the example app follow these instructions:

```bash
# Clone package
~$ git clone https://github.com/genexu/react-native-pie-chart.git

# Install dependencies
~$ cd react-native-pie-chart/example
~$ npm install

# Run simulator
~$ npm run start
```

## Upgrade Guide

### From 3.x.x to 4.x.x

New format for `series` (object-based) and unified `cover` prop.

### From 2.x.x to 3.x.x

Migration from `@react-native-community/art` to `react-native-svg`.

### From 1.x.x to 2.x.x

Rename `chart_wh` to `widthAndHeight`.

## v3 Legacy API

If you still use v3 API:

```ts
import PieChart from 'react-native-pie-chart/v3api'
```

```ts
export type Props = {
  widthAndHeight: number
  series: number[]
  sliceColor: string[]
  coverFill?: string | null
  coverRadius?: number
  style?: StyleProp<ViewStyle>
}
```