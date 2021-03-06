# react-prop-log

A simple React performance and debugging helper. Drop into a component and monitor props changes in the console.

## Installation

`npm i --save-dev react-prop-log`

## Usage

`propLog` is a function that'll wrap a component and log any props changes whenever the `componentDidUpdate` lifecycle method executes. `propLog` is a higher-order component (HOC) so you'll add it similarly to Redux's `connect`.

```js
import { propLog } from 'react-prop-log';
/* -- Your component code here  -- */
export default propLog(YourComponentName);
```

To ensure you see all props changes when debugging, make sure `propLog` is the innermost function if your component is nested in multiple HOCs.

```js
// do this
export default exampleHOC(anotherExampleHOC(propLog(YourComponentName)));

// not this
export default propLog(exampleHOC(anotherExampleHOC(YourComponentName)));
```

`logChangedProps` is the actual logger, and can be imported separately for greater control on where in the React lifecycle it is triggered. It expects a new set of props & your component instance.

```js
import { logChangedProps } from 'react-prop-log';

class YourComponent extends React.Component {
  /* -- Your component code here  -- */
  componentDidUpdate(nextProps) {
    logChangedProps(nextProps, this);
  }
  /* -- Your component code here  -- */
}

export default YourComponent;
```

## Development

See [CONTRIBUTING](https://github.com/domain7/react-prop-log/blob/master/CONTRIBUTING.md) for information on working with the codebase.
