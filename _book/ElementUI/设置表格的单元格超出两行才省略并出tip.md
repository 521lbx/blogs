### 设置表格的单元格超出两行才省略并出tip
* 1.更改radui
```
handleCellMouseEnter(event, row) {
    const table = this.table;
    const cell = getCell(event);

    if (cell) {
    const column = getColumnByCell(table, cell);
    const hoverState = table.hoverState = {cell, column, row};
    table.$emit('cell-mouse-enter', hoverState.row, hoverState.column, hoverState.cell, event);
    }

    // 判断是否text-overflow, 如果是就显示tooltip
    const cellChild = event.target.querySelector('.cell');
    if (!(hasClass(cellChild, 'el-tooltip') && cellChild.childNodes.length)) {
    return;
    }
    const range = document.createRange();
    range.setStart(cellChild, 0);
    range.setEnd(cellChild, cellChild.childNodes.length);
    const rangeWidth = range.getBoundingClientRect().width;
    const rangeHeight = range.getBoundingClientRect().height;
    const padding = (parseInt(getStyle(cellChild, 'paddingLeft'), 10) || 0) +
    (parseInt(getStyle(cellChild, 'paddingRight'), 10) || 0);
    if (((rangeWidth + padding > cellChild.offsetWidth || cellChild.scrollWidth > cellChild.offsetWidth) || (rangeHeight + padding > cellChild.offsetHeight || cellChild.scrollHeight > cellChild.offsetHeight)) && this.$refs.tooltip) {
    const tooltip = this.$refs.tooltip;
    // TODO 会引起整个 Table 的重新渲染，需要优化
    this.tooltipContent = cell.innerText || cell.textContent;
    tooltip.referenceElm = cell;
    tooltip.$refs.popper && (tooltip.$refs.popper.style.display = 'none');
    tooltip.doDestroy();
    tooltip.setExpectedState(true);
    this.activateTooltip(tooltip);
    }
},
```
* 2.设置样式
```
.el-table__row .cell {
    text-overflow: -o-ellipsis-lastline;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    line-clamp: 2;
    -webkit-box-orient: vertical;
}
.cell.el-tooltip {
    white-space: unset;
}
```


