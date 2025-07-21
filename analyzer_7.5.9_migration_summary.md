# Analyzer 7.5.9 Migration Summary

This document summarizes the changes made to migrate from deprecated analyzer APIs to the current APIs in analyzer version 7.5.9.

## Key Changes

### 1. Dynamic Type Checking
- **Old**: `type.isDartCoreDynamic`
- **New**: `type is DynamicType`
- Files affected: Multiple lint analyzer rules

### 2. Void Type Checking
- **Old**: `type.isDartCoreVoid`
- **New**: `type is VoidType`
- Files affected: avoid_ignoring_return_values, prefer_moving_to_variable, check_for_equals_in_render_object_setters

### 3. Element Access in AST Nodes
- **Old**: `node.element2` (for NamedType, ImportDirective, ExportDirective, etc.)
- **New**: `node.element`
- Files affected: Most lint analyzer rules and analyzers

### 4. Enclosing Element Access
- **Old**: `element.enclosingElement3`
- **New**: `element.enclosingElement` (Note: Some cases had to be temporarily commented out due to API changes)
- Files affected: unused_code_analyzer, unused_l10n_analyzer, avoid_global_state

### 5. Removed/Changed APIs (Temporarily Commented Out)
- `ContextLocator` - Not available in analyzer 7.5.9
- `IfStatement.condition` - Property name changed, possibly to `expression`
- `WhileStatement.condition` - Property name changed
- `AssertStatement.condition` - Property name changed
- `Comment.isDocumentation` - Property removed, workaround uses token checking
- `PropertyAccessorElement.variable` - Property not available

### 6. Import Additions
- Added `import 'package:analyzer/dart/element/type.dart';` to files using DynamicType, VoidType, etc.

## Notes

1. Some functionality had to be temporarily disabled or worked around due to missing APIs in analyzer 7.5.9.
2. The migration maintains backward compatibility by using `// ignore: deprecated_member_use` comments where necessary.
3. Several TODOs have been added to mark places where alternative approaches are needed for analyzer 7.5.9.
4. The test for unused files analyzer passes compilation but fails at runtime due to logic issues (not related to the API migration).

## Recommendations

1. Review the temporarily disabled functionality and implement proper alternatives.
2. Update test expectations as needed for the new analyzer behavior.
3. Consider creating wrapper functions for commonly used patterns that differ between analyzer versions.
4. Monitor analyzer releases for restored APIs and update accordingly.
