# Restore window geometry

`windowGeometry` is a struct with x, y, width, and height fields that all have the ability to know if they've been set yet.

Code taken from https://github.com/fourtf/chatterino2/blob/e58c5ec11bf16be91da03495bc86958a588d4027/src/widgets/window.cpp#L117-L141

```cpp
void restoreGeometry()
{
    bool doSetGeometry = false;
    QRect loadedGeometry;
    if (!this->windowGeometry.x.isDefaultValue() && !this->windowGeometry.y.isDefaultValue()) {
        loadedGeometry.setX(this->windowGeometry.x);
        loadedGeometry.setY(this->windowGeometry.y);
        doSetGeometry = true;
    }

    if (!this->windowGeometry.width.isDefaultValue() &&
        !this->windowGeometry.height.isDefaultValue()) {
        loadedGeometry.setWidth(this->windowGeometry.width);
        loadedGeometry.setHeight(this->windowGeometry.height);
    } else {
        loadedGeometry.setWidth(1280);
        loadedGeometry.setHeight(720);
    }

    if (doSetGeometry) {
        // Restore position and size
        this->setGeometry(loadedGeometry);
    } else {
        // Restore size
        this->resize(loadedGeometry.width(), loadedGeometry.height());
    }
}
```
