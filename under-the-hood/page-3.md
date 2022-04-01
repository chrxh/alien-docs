# Architecture

## Overview

At the coarsest level, the source code can be structured into targets (libraries and executables) and their dependencies. The _Base_ library is used by all others and therefore is not separately marked with dependency arrows.

![Dependencies of libraries (orange) and executables (green)](../.gitbook/assets/packages.svg)

## Engine

![Engine classes and their dependencies](../.gitbook/assets/engine.svg)

## GUI

![Gui classes and their dependencies](../.gitbook/assets/gui.svg)
