# React Patterns & Best Practices

## Component Structure
- Use functional components with hooks
- One component per file
- Keep components focused and small

## Hooks Usage
- Use useCallback to memoize callback functions
- Use useMemo for expensive computations
- Use useEffect for side effects only
- Never call hooks conditionally

## State Management
- Keep state as close as possible to where it's used
- Lift state only when necessary
- Consider Context API for shared state
- Use reducers for complex state logic

## Performance
- Use React.memo for expensive components
- Split code with React.lazy and Suspense
- Profile using React DevTools Profiler

## Accessibility
- Use semantic HTML elements
- Add aria-labels for interactive elements
- Ensure keyboard navigation works
- Test with screen readers
