JoRecyclerViewAdapter
============

This adapter is for the RecyclerView to easily manage headers, putters, and items.
also It contains useful features for recyclerview.
- load more items bottom
- empty view
- quick return UI pattern

Simple usage
```java
adapter = new JoRecyclerAdapter<Integer>(new JoRecyclerAdapter.Params()
                .setRecyclerView(rcv)
                .setItemViewHolderCls(BlankVHolder.class)
        );
        
rcv.setAdapter(adapter);
```

Before setting adapter, Create ViewHolder extending JoViewHolder<T>
T is model type.

```java
@LayoutMatcher(layoutId = R.layout.item_padding)
public class BlankVHolder extends JoViewHolder<String> {

    public BlankVHolder(View itemView) {
        super(itemView);
    }

    @Override
    public void onViewCreated() {
        //initiating views.
        ButterKnife.bind(this, itemView);
    }

    
    @Override
    public void onBind(String m, int pos, int absPos) {
        String param1 = getRcvParams().getParam("param1"); //get paramter
        int param2 = getRcvParams().getParam("param2");
        float param3 = getRcvParams().getParam("param3");
        Context context = getContext();
        super.onBind(m, pos, absPos);
    }
}

```

If you need set header view or footer view item, Check it below.
Header and Footer also follows JoViewHolder 
```java
adapter = new JoRecyclerAdapter<String>(new JoRecyclerAdapter.Params()
                .setRecyclerView(rcv)
                .addParam("TYPE", type)
                .setHeaderViewHolderCls(BlankVHolder.class)
                .setFooterViewHolderCls(BlankVHolder.class)
                .setItemViewHolderCls(ConsultantSalaryVHolder.class)
                .setEmptyView(R.id.layerEmpty_vContents)
                .setBottomLoading(getActivity().getLayoutInflater().inflate(R.layout.layer_footer_loading, null), new FooterLoadingListener() {
                    @Override
                    public void onFooterLoading() {
                        adapter.getLastItem(); // get last item
                    }
                })
                
adapter.addHeaderItem("SOMEHEADER DATA");
adapter.addFooterItem("SOMEFOOTER DATA");

rcv.setAdapter(adapter);
```

Use QuickReturn pattern in RecyclerView
```java
Prepare a single view for QuickReturn in the activity.
View vQuickReturn = ...;
QuickReturnViewInitializor.init(recyclerview, vQuickReturn);
```


