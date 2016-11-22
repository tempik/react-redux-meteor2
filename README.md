React Redux Meteor
=========================

React bindings for [Redux](https://github.com/reactjs/redux) + [Meteor](https://github.com/meteor/meteor). 

Performant and flexible.

> This project is forked from [react-redux](https://github.com/reactjs/react-redux) and will not send PR to the original repo because it's for Meteor ONLY.

## Installation

React Redux Meteor requires **React 0.14 or later.**

```
npm install --save react-redux-meteor
```

## Documentation

- [Redux: Usage with React](http://redux.js.org/docs/basics/UsageWithReact.html)
- [API](docs/api.md#api)
  - [`<Provider store>`](docs/api.md#provider-store)
  - [`connect([mapTrackerToProps], [mapStateToProps], [mapDispatchToProps], [mergeProps], [options])`](docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options)
- [Troubleshooting](docs/troubleshooting.md#troubleshooting)

## What's new in `react-redux-meteor`

`mapTrackerToProps` is now the first argument of `connect()`

> The Tracker props are NOT stored in redux store because they are client read-only and reactive. You can  change Tracker props by calling Meteor methods.

```
const mapTrackerToProps = (state, props) => {
  if (Meteor.subscribe('posts').ready()) {
    return { posts: Posts.find().fetch() };
  }
  return { posts: [] };
};

const mapStateToProps = (state, props) => {
  return {
    // ...
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    // ...
  };
};

export default connect(
  mapTrackerToProps,
  mapStateToProps,
  mapDispatchToProps
)(PostList);
```
If you don't want to use Tracker data as props, just put null for the first argument
```
export default connect(
  null,
  mapStateToProps,
  mapDispatchToProps
)(PostList);
```
## Q & A
#### Why not use createContainer in Meteor tutorial?

If you use `createContainer` and `connect` for `react-redux`, you have to create containers twice. It might affect (Not sure) the performance. But with `react-redux-meteor`, you will only create container once.

#### Why not use react-komposer?

The purpose of developing `react-redux-meteor` is for the users who are already familiar with `react-redux`. It just adds a parameter to `connect()` and very easy to use. However, if you never use `react-redux`, you can try either of them. `react-komposer` is also a good choice.

#### Will react-redux-meteor be merged to react-redux?

No. Because `react-redux-meteor` uses Tracker behind the scene which is especially for Meteor. However, if the official react-redux has updates, I will merge the updates into react-redux-meteor.
