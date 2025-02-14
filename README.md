# React Native useEffect Async Cleanup Issue

This repository demonstrates a common issue in React Native applications involving the `useEffect` hook and asynchronous operations.  The problem arises when an asynchronous function is used within `useEffect`, and the component unmounts before the async operation completes. This can lead to unexpected behavior, memory leaks, or errors.

The `useEffectBug.js` file shows the problematic code.  `useEffectSolution.js` demonstrates a solution using the `return` statement within the `useEffect` cleanup function to ensure proper cleanup, even if the component unmounts prematurely. This is done by checking if the component is still mounted before doing the cleanup action, using the `mounted` state variable to accomplish this.

## Problem
The problem is that if the component unmounts quickly, the cleanup function provided to useEffect might not run. For example, this is common with fetch requests where the component unmounts before the request is completed. This can lead to problems with things like memory leaks, especially with larger datasets or long running processes.

## Solution
The solution demonstrates a safer approach for performing asynchronous actions in useEffect by ensuring the async action completes or is cancelled in the process. The use of a cancellation variable provides a mechanism to avoid doing cleanup tasks when the component is unmounted before completing the async process.