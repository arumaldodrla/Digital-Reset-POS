# Safe Refactor and Extension Guide

## 1. Overview

This guide provides instructions for AI agents on how to safely refactor and extend the Universal Offline POS system. The goal is to ensure that all changes are made in a way that is consistent with the existing architecture and does not introduce any breaking changes.

## 2. Guidelines

### Do not delete or rewrite critical architecture docs

The documentation in the `/docs/10-architecture` directory is critical to the understanding of the system. Do not delete or rewrite these documents without a clear understanding of the implications.

### Add new docs in a consistent location and format

When adding new documentation, ensure that it is placed in the correct directory and follows the existing format and style.

### Always update ERD and schema docs when the DB changes

If you make a change to the database schema, you must update the "Domain Model and ERD" and "Database Schema Reference" documents to reflect the changes.

### Follow existing patterns and conventions

When adding new features or refactoring existing code, always follow the existing patterns and conventions of the project. This includes coding style, file structure, and component design.

### Write tests for all new features

All new features must be accompanied by a set of tests that verify the functionality and prevent regressions.
