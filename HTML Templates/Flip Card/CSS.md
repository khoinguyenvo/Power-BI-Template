```CSS
.card {
  width: 440px;
  height: 240px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-smoothing: antialiased;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
  -moz-osx-font-smoothing: grayscale;
}

.card-inner {
  width: 100%;
  height: 100%;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 0.9s;
}

.card:hover .card-inner {
  transform: rotateY(180deg);
}

.card-front,
.card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  transform: translateZ(0);
}

.card-front {
  background-color: transparent;
  display: flex;
  align-items: center;
  border-radius: 8px;
  justify-content: center;
  font-size: 16px;
  transform: rotateY(0deg);
}

.card-back {
  background-color: transparent;
  display: flex;
  align-items: center;
  border-radius: 8px;
  justify-content: center;
  font-size: 16px;
  transform: rotateY(180deg);
}
.card-header {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 10px;
}

.card-header .caption {
    font-weight: 600;
    font-size: 24px;
    color: #1B2940;
}

.card-header .icon {
    font-size: 24px;
    color: #1B2940;
}

table {
  width: 90%;
  border-collapse: collapse;
}

caption{
  text-align: left
}

table, th, td {
  border-bottom: 1px solid transparent;
}
  
th, td {
  padding: 8px;
  text-align: center;
}
  
th {
   background-color: transparent;
}
.icon {
    margin-right: 8px;
}
```
