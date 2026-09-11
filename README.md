# Procedural Forest System

A rule-based procedural vegetation system developed in **Houdini** for environment-driven distribution and spatial interaction between trees, bushes, and grass.

The system uses terrain-derived environmental attributes and sequential vegetation dependencies to generate a procedural forest rather than treating each vegetation layer as an independent scatter.

![Hero](../Media/hou_ue.jpg)

## Overview

The system determines **where and under what conditions vegetation is distributed** across the terrain.

It does not generate the vegetation assets themselves. Tree, bush, and grass geometries are provided as inputs and distributed by the system according to procedural rules.

### Core Flow

```text
Terrain
   ↓
Environment Attributes
   ↓
General Density
   ↓
Tree Layer
   ↓
Tree Influence
   ↓
Bush Layer
   ↓
Bush Influence
   ↓
Grass Layer
   ↓
Final Vegetation
```

## Main Features

* Environment-driven vegetation distribution
* Height- and slope-based vegetation suitability
* Procedural humidity generation
* General vegetation density mask
* Add / Remove and Overwrite custom masks
* Tree, bush, and grass distribution layers
* Tree-to-bush and tree-to-grass spatial influence
* Bush-to-grass spatial influence
* Independent tree influence controls for bushes and grass
* Procedural density variation
* Vegetation scale variation
* Cluster and point-separation controls
* HeightField debug and visualization outputs
* Houdini Engine integration testing with Unreal Engine

## System Structure

The system is organized into modular internal stages:

```text
Terrain Masks + General Density
              ↓
        Tree Density
              ↓
         Tree Scatter
              ↓
        Tree Influence
              ↓
     Bush + Bush Influence
              ↓
            Grass
```

The internal stages are organized using Houdini subnets to keep the high-level network readable and separate system architecture from implementation details.

## Environmental Logic

The general vegetation suitability is driven by terrain and procedural environmental data.

```text
Height
   ↓
Humidity
   ↓
Base Density
   ↓
Custom Mask Operations
   ↓
density_mask
```

The vegetation layers then apply additional rules and spatial influences.

### Vegetation Dependencies

```text
Trees
 ├── tree_influencebush  → Bush Density → Bushes
 │
 └── tree_influencegrass → Grass Density

Bushes
      ↓
bush_influence
      ↓
Grass Density
```

This creates sequential dependencies between vegetation layers instead of independent scattering.

## Inputs

### Terrain

Required HeightField / voxel-based terrain used for environmental analysis and vegetation distribution.

### Custom Masks

* Add / Overwrite Mask
* Remove Mask

### Vegetation Geometry

* Tree geometry
* Bush geometry
* Grass geometry

## Outputs

* Scattered Trees
* Scattered Bushes
* Scattered Grass
* Visualized Terrain

## Houdini & Unreal Engine

**Houdini:** 20.0.547
**Unreal Engine:** 5.2.1

The system has been tested for Unreal Engine integration through Houdini Engine.

For reliable Unreal results, vegetation meshes used within the same vegetation layer should follow a consistent ground-relative pivot/origin convention.

Very large terrain inputs may not be handled reliably during Unreal Engine integration and may result in instability or application crashes depending on scene complexity and available system resources.

## Documentation

The full documentation covers:

* System architecture
* Environmental model
* Vegetation generation logic
* Attribute flow
* Interaction model
* HDA parameters
* Custom mask implementation
* Generation process
* Houdini visualization
* Unreal Engine integration
* Limitations
* Future improvements

[**Full Documentation:**](./Documentation/Procedural_Forest_System_Documentation.md)

## Project Focus

This project explores:

* Procedural environment design
* Rule-based worldbuilding
* Attribute-driven systems
* HeightField workflows
* Spatial influence systems
* Procedural vegetation distribution
* HDA design
* Houdini → Unreal Engine workflows

## Status

**Version:** 1.0.0
**Status:** Initial release

## License

This tool is provided for **non-commercial, educational, and personal use**.

The system was developed using **Houdini Apprentice** and is distributed as a non-commercial Houdini Digital Asset (`.hdanc`).

## Credits

**Tool Development & Documentation:** Mina D.

**Development Assistance:** AI-assisted learning and documentation workflow support provided through OpenAI ChatGPT.
