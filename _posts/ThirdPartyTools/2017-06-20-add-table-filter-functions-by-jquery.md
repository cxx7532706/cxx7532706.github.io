---
layout: post
category : ThirdPartyTools
tagline: "Supporting tagline"
tags : [Front-End, ThirdPartyTools, Bootstrap-table, Jquery]
---
{% include JB/setup %}

This post will talk about how to do table filter function by using Jquery and Bootstrap-table. For those who doesn't know about Bootstrap-table, please look at my previous article first.
["Bootstrap-Table"]({% post_url ThirdPartyTools/2017-06-19-Powerful-Grid-Tool-Bootstrap_Table %})

First I'll show you how the finished functions look like.

### Original Table:
<img src="/assets/photos/Table-Filter-1.png" alt="Bootstrap-table" style="width: 630px; margin: 0 auto; display:block;"/> 

### Filtered Table:
<img src="/assets/photos/Table-Filter-2.png" alt="Bootstrap-table" style="width: 630px; margin: 0 auto; display:block;"/>

I just added a DateTime filter because of my project need, but you could add whatever functions you want by the same way.

The concept of achieving this is by a method from Bootstrap-table `$table.bootstrapTable('load',filterData())`, this method will load/reload the content for table to display.

So what we'll do next, is filter the content by input boundaries, and load the filtered content to table. Then you'll get what you want!

~~~
    $(function(){
        $searchButton.click(function(){
            $table.bootstrapTable('load',filterData());
        });
    }
    function filterData(){
        var begin = $('#startDate').val(), end = $('#endDate').val();
        var rows = [];
        @foreach (var item in Model){
            <text>
                var pDate = new Date(@item.PurchaseDate.ToString("yyyy,MM-1,dd"));
                var sDate = new Date(begin);
                sDate.setTime(sDate.getTime() + sDate.getTimezoneOffset()*60*1000);
                var eDate = new Date(end);
                eDate.setTime(eDate.getTime() + eDate.getTimezoneOffset()*60*1000);
            if(pDate >= sDate && pDate <= eDate)
            {
                var comment = new String("@item.comment");
                var s = new String("@item.Product.Name" + "(" + "@item.Product.Purity" + ")");
                var supplierName = new String("@item.Supplier.SupplierName");
                var recordId = new String("@item.PurchaseRecordId");

                var funcString =
                    '<a href="/PurchaseRecords/Edit/' + recordId + '">编辑记录</a> | ' +
                    '<a href="/PurchaseRecords/Delete/' + recordId + '">删除记录</a>';

                rows.push({
                    Date: "@item.PurchaseDate.ToString("yyyy-MM-dd")",
                    Price: @item.PricePerTon,
                    Quantity: @item.Quantity,
                    TotalPrice: @item.TotalPaidPrice,
                    PaidBackPrice: @item.PaidBackPerTon,
                    PaidBackTotal: @item.TotalPaidBack,
                    Comment: comment,
                    Product: s,
                    Supplier: supplierName,
                    Functions: funcString
                });
            }
            </text>
        }
        return rows;
    }
~~~
 