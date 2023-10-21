# Load list of data with PAGES - React Naive

## Types
```js
export const TYPES = {
    LOAD: "TYPES/LOAD",
    REFRESH: "TYPES/REFRESH",
    LOAD_MORE: "TYPES/LOAD_MORE",
    SUCCESS: "TYPES/SUCCESS",
    LOAD_MORE_SUCCESS: "TYPES/LOAD_MORE_SUCCESS",
    FAILED: "TYPES/FAILED",
};
```

## Action
```js
const getListData = ({ currentPage, action }) => async (dispatch, getState) => {
    dispatch({ type: action === "loadMore" ? TYPES.LOAD_MORE : action === "refresh" ? TYPES.REFRESH : TYPES.LOAD });
    try {
        const apiResponse = new Array(30).fill(Math.random());
        await delay(1000)
        dispatch({
            type: action === "loadMore" ? TYPES.LOAD_MORE_SUCCESS : TYPES.SUCCESS,
            payload: {
                data: apiResponse,
                currentPage,
                totalPages: 6,
            },
        });
    } catch (e) {
        dispatch({
            type: TYPES.FAILED,
            payload: e,
        });
    }
};

export const DummyFunctions = {
    getListData
}
```
## Reducer
```js
import { TYPES } from "../../utils/constants";

const initialState = {
  list: {
    loading: false,
    refreshing: false,
    loadMore: false,
    data: [],
    currentPage: 1,
    totalPages: 3,
    error: null,
  },
};

export default (state = initialState, action) => {
  switch (action.type) {
      case TYPES.LOAD:
          return {
              ...state,
              list: {
                  ...state.list,
                  loading: true,
                  error: null,
              },

          };
      case TYPES.REFRESH:
          return {
              ...state,
              list: {
                  ...state.list,
                  refreshing: true,
                  error: null,
              },

          };
      case TYPES.LOAD_MORE:
          return {
              ...state,
              list: {
                  ...state.list,
                  loadMore: true,
                  error: null,
              },
          };
      case TYPES.SUCCESS:
          return {
              ...state,
              list: {
                  ...state.list,
                  loading: false,
                  refreshing: false,
                  data: action.payload.data,
                  currentPage: action.payload.currentPage,
                  totalPages: action.payload.totalPages,
                  error: null,
              },
          };
      case TYPES.LOAD_MORE_SUCCESS:
          return {
              ...state,
              list: {
                  ...state.list,
                  loadMore: false,
                  data: [
                      ...state.list.data,
                      ...action.payload.data,
                  ],
                  currentPage: action.payload.currentPage,
                  totalPages: action.payload.totalPages,
                  error: null,
              },
          };
      case TYPES.FAILED:
          return {
              ...state,
              list: {
                  ...state.list,
                  error: action.payload,
                  loading: false,
                  refreshing: false,
                  loadMore: false,
              },
          };

      default :
          return state;
  }
}
```

## Component
```js
import { ActivityIndicator, FlatList, RefreshControl, Text, View } from "react-native";
import React from "react";
import Loader from "./Loader";

export default ({
                  data = [],
                  loading = true,
                  refreshing = false,
                  provider: { getListData },
                  lastPage,
                  currentPage,
                  loadMore = false,
                }) => {

    const renderItem = ({ item }) => {
        return (
            <View>
                {valuesToExtract?.map((val)=>(
                    <Text style={{ color: "black" }}>{item[val]}</Text>
                ))}
            </View>
        );
    };
    
  const itemSeparator = () => (
    <View
      style={{
        height: 0.4,
        marginHorizontal: 10,
        marginVertical: 5,
        backgroundColor: "#000",
        opacity: 0.4,
      }}
    />
  );
  const onRefresh = () => getListData({ currentPage: 1, action: "refresh" });
  const onEndReached = () => {

    if (currentPage < lastPage) {
      getListData({ currentPage: currentPage + 1, action: "loadMore" });
    }
  };
  const loadMoreComp = () => (
    <View style={{ height: 100 }}>
      {loadMore && <ActivityIndicator size={'small'} color="#000" />}
    </View>
  );
  return (
    <View style={{ flex: 1, height: "100%" }}>
      {
        loading
          ? <Loader visible={loading} />
          : (data.length === 0) ? <Text>No Data Available</Text>
            : <FlatList
              data={data}
              renderItem={renderItem}
              ItemSeparatorComponent={itemSeparator}
              keyExtractor={(item, index) => index.toString()}
              refreshing={refreshing}
              onRefresh={onRefresh}
              onEndReached={onEndReached}
              onEndThreshold={0.5}
              onEndReachedThreshold={0.04}
              ListFooterComponent={loadMoreComp}
              refreshControl={
                <RefreshControl
                  refreshing={refreshing}
                  onRefresh={onRefresh}
                />
              }
            />
      }
    </View>
  );
};
```

## Usage
```js
import { SafeAreaView } from "react-native";
import ListBuilder from "../../components/ListBuilder";
import { connect } from "react-redux";
import { DummyFunctions } from "../../redux/action/dummyAction";

export default connect((state) => ({
  loading: state.dummy.list?.loading ?? false,
  refreshing: state.dummy.list?.refreshing ?? false,
  loadMore: state.dummy.list?.loadMore ?? false,
  data: state.dummy.list?.data ?? [],
  currentPage: state.dummy.list?.currentPage ?? 1,
  totalPages: state.dummy.list?.totalPages ?? 1,
  error: state.dummy.list?.error ?? null,
}), {
  getListData: DummyFunctions.getListData,
})(({
      loading,
      refreshing,
      loadMore,
      data,
      currentPage,
      totalPages,
      error,
      getListData,
    }) => {
  return (
    <SafeAreaView style={{ flex: 1 }}>
      <ListBuilder
        data={data}
        loading={loading}
        refreshing={refreshing}
        provider={{ getListData }}
        lastPage={totalPages}
        currentPage={currentPage}
        loadMore={loadMore}
        valuesToExtract={['name','city']}
      />
    </SafeAreaView>
  );
});
```
