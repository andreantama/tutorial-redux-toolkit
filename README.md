# TUTORIAL REDUXJS/TOOLKIT
## Create Slices of Initial state Data & Reducer
1. Install reduxjstoolkit
```bash
npm install @reduxjs/toolkit --save
```
2. Buat file index.js di ./src/store/index.js
3. Buka file index.js dan tambahkan code.
```javascript
import {createSlice} from '@reduxjs/toolkit'
```
1. createSlice digunakan untuk membagi global state supaya dapat di handle di file terpisah.
```javascript
import {createSlice} from "@reduxjs/toolkit";
const initialStateToastData = {
success: false,
error: false,
info: false,
warning:false,
};
createSlice({
name: 'toastData',
intialStateToastData,
});
```
1. Buat reducer untuk dapat memanipulasi intialState
```javascript
import {createSlice} from "@reduxjs/toolkit";
const initialStateToastData = {
success: false,
error: false,
info: false,
warning:false,
};
createSlice({
name: 'toastData',
intialStateToastData,
	reducers: {
		showSuccess(state, payload) {
			state.success = payload;
		},
		showError(state, payload) {
			state.error = payload;
		},
		showInfo(state, payload) {
			state.info = payload;
		},
		showWarning(state, payload) {
			state.warning = payload;
		},
	}
});
```
## Connecting ReduxToolkit.
1. Return createSlice yang kita buat kedalah configureStore, yang mana configureStore dapat auto merge beberapa state
```javascript
import {createSlice, configureStore} from "@reduxjs/toolkit";
const initialStateToastData = {
success: false,
error: false,
info: false,
warning:false,
};
const dataToastSlice = createSlice({
name: 'toastData',
intialStateToastData,
	reducers: {
		showSuccess(state, payload) {
			state.success = payload;
		},
		showError(state, payload) {
			state.error = payload;
		},
		showInfo(state, payload) {
			state.info = payload;
		},
		showWarning(state, payload) {
			state.warning = payload;
		},
	}
});
const store = configureStore({
    reducer: {
      toast: dataToastSlice.reducer
    }
  });
export default store;
```
1. Return action tanpa harus membuat identifiernya pada redux normal.
```javascript
import {createSlice, configureStore} from "@reduxjs/toolkit";
const initialStateToastData = {
success: false,
error: false,
info: false,
warning:false,
};
const dataToastSlice = createSlice({
name: 'toastData',
intialStateToastData,
	reducers: {
		showSuccess(state, payload) {
			state.success = payload;
		},
		showError(state, payload) {
			state.error = payload;
		},
		showInfo(state, payload) {
			state.info = payload;
		},
		showWarning(state, payload) {
			state.warning = payload;
		},
	}
});
const store = configureStore({
    reducer: {
      toast: dataToastSlice.reducer
    }
  });
export const toastAction = dataToastSlice.actions;
export default store;
```
1. Untuk memasang global store, Pasang Provider component didalam file src/index.js.
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import './index.css';
import App from './App';
import store from './store/index';
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```
1. Untuk mengakses state yang tersimpan bisa seperti ini.
```javascript
import { useSelector, useDispatch } from 'react-redux';
const toast = useSelector((state) => state.counter.toast);
```
1. Untuk mengakses action yang terdaftar bisa seperti ini.
```javascript
import { useSelector, useDispatch } from 'react-redux';
import { toastActions } from '../store/index';
const dispatch = useDispatch();
dispatch(toastActions.showSuccess(10)); // { type: SOME_UNIQUE_IDENTIFIER, payload: 10 }
```